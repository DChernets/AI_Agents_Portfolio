# Wildberries FBS Supply Chain & Fulfillment Automation

**Production autonomous system for marketplace order processing, multi-warehouse supply grouping, sticker & QR document generation, and fulfillment dispatch.**

---

## Business context

The client is an e-commerce brand operating on **Wildberries** (the largest marketplace in Russia / CIS), selling electronics, personal shavers, and trimmers under the *Higher Energy* brand. The business operates under the **FBS (Fulfillment by Seller)** model, shipping out 100–300+ orders daily across 24 regional logistics hubs.

Under marketplace rules, FBS orders must be collected, grouped by warehouse, packed, labeled, and transferred to delivery status every morning by 10:00 MSK. Missing deadlines results in heavy penalties, cancellation ratings, or account suspension.

Previously, operations managers had to:
1. Manually download assembly tasks from the Wildberries web portal for every city.
2. Group hundreds of orders by regional distribution centers (Moscow, Saint Petersburg, Ekaterinburg, Kazan, Novosibirsk, Rostov, Irkutsk, etc.).
3. Manually create supply batches and attach individual orders.
4. Manually generate boxes (`trbx` cargo spaces) for pickup points (PVZ) while navigating undocumented marketplace API quirks.
5. Download separate barcode labels and QR codes, opening dozens of PDF files.
6. Calculate itemized write-offs manually for accounting in MoySklad.
7. Coordinate back-and-forth in messenger chats with the 3PL fulfillment warehouse team every morning under tight time pressure.

---

## Delivered workflow

The system runs autonomously on a production Linux VPS via precise `systemd` timers:

```mermaid
flowchart TD
    subgraph Phase 1 ["Phase 1: Order Ingestion & Supply Assembly (09:30 MSK)"]
        A["WB Orders API (GET /orders/new)"] --> B["Active Orders Filter (Drop cancellations)"]
        B --> C["Regional Grouping (24+ FBS Warehouses)"]
        C --> D["Race-Guard Supply Creator (Deduplication)"]
        D --> E["Batch Order Attachment (PATCH /orders)"]
        E --> F["Logistics Rules (Auto-trbx for PVZ)"]
        F --> G["Post-Step Verification (_verify_phase1)"]
        G --> H["Telegram Assembly Report (09:30)"]
    end

    subgraph Phase 2 ["Phase 2: Delivery Commit, Docs & Fulfillment Dispatch (09:44 MSK)"]
        I["Supplies in DB"] --> J["WB API Commit (PATCH /deliver)"]
        J --> K["Download Official WB Barcodes & QRs"]
        K --> L["Sticker Compiler (Grouped by Article + Separators)"]
        K --> M["Supply QR Compiler (58x40 mm Sheets)"]
        J --> N["Inventory Write-off Calculation (TXT Summary)"]
        L & M --> O["PDF Integrity & Page Verification (pypdf)"]
        O & N --> P["Telegram Bot Dispatch (Retry Loop)"]
        P --> Q["30-Day Rolling Cleanup (Logs, Docs, SQLite)"]
    end

    Phase 1 -->|Wait buffer for physical picking| Phase 2
```

### 1. Phase 1: Ingestion & Assembly (09:30 MSK)
- **Ingestion & Filtering:** Fetches all pending assembly tasks from Wildberries Marketplace API v3 (`GET /api/v3/orders/new`), cross-checks real-time order statuses to immediately drop buyer cancellations, and isolates FBS delivery tasks.
- **Multi-Warehouse Routing:** Groups orders across 24+ regional warehouses (Obukhovo, Ekaterinburg, Kazan, Rostov, Krasnodar, Novosibirsk, Irkutsk, etc.).
- **Race-Guard Deduplication:** If an operator already created a partial supply manually in the portal, the system recognizes the existing supply and merges new orders instead of creating duplicate batches.
- **Logistics Specialization:** Automatically allocates required transit cargo boxes (`trbx`) for pickup points (Koeldino PVZ) while skipping redundant boxes for sort centers (SC).
- **Post-Step Verification:** Re-queries the WB API (`_verify_phase1`) to verify that 100% of orders are registered in the supplies, self-heals missing cargo boxes, and confirms zero uncollected orders remain in `orders/new`.
- **Status Broadcast:** Emits a structured morning summary to the fulfillment Telegram channel with warehouse order breakdowns.

### 2. Phase 2: Delivery Commit, Document Pipeline & Fulfillment (09:44 MSK)
- **Irreversible Commit:** Executes `PATCH /api/v3/supplies/{id}/deliver` across all supplies and downloads official WB barcodes.
- **Targeted Sticker Generation:** Compiles a unified multi-page PDF (`{DD.MM} стикеры.pdf`):
  - Orders are grouped by seller article.
  - Each product batch is preceded by a high-contrast separator label framed in 58×40 mm: **[Article name / N pcs]**.
  - Followed by exactly `N` official WB order QR stickers (58×40 mm).
- **Unified Supply QR PDF:** Generates `{DD.MM} поставки.pdf` containing one official 58×40 mm supply barcode per warehouse for warehouse intake scanning.
- **Inventory Write-off Export:** Compiles `{DD.MM} списание.txt` containing itemized totals and per-city breakdowns for fast 1-click accounting in MoySklad.
- **Document Integrity Auditing:** Uses `pypdf` to parse and validate every generated PDF before delivery, guaranteeing that page counts match `(N articles + M orders)` and supply counts.
- **Resilient Telegram Delivery:** Sends all files and summaries directly into the 3PL fulfillment group chat with automatic retries and exponential backoff.
- **Automated Lifecycle & Retention:** Rotates logs daily and enforces a strict 30-day retention window: files older than 30 days in `logs/` and `data/documents/` as well as historical SQLite `run_events` are automatically purged.

---

## Engineering decisions & reliability

### Live production without Sandbox
Wildberries provides no sandbox environment for marketplace FBS supplies. Mutating endpoints (especially `PATCH /deliver`) are irreversible and trigger real financial penalties if orders are marked delivered without goods ready.
- Designed a multi-tier safety execution model: `OFF` -> `READ_ONLY` -> `DRY_RUN` -> `PILOT` -> `PILOT_DELIVER` -> `LIVE`.
- Allowed incremental testing on live stores without risking unfulfilled order penalties.

### Reverse-engineering marketplace API logistics
Wildberries documentation states that a drop-off point (`shippingPointId`) must be selected. Through API spikes, discovered that Wildberries automatically registers the destination sorting center during intake physical barcode scanning. Bypassed fragile private portal endpoints and relied on the robust public Marketplace v3 API.

### Resilient, throttled API communication
Wildberries imposes a strict rate limit of 300 requests/min. The client incorporates a 250ms interval throttler, backoff retries on HTTP 429/500/502/503, and captures full structured response payloads on HTTP 4xx/5xx to eliminate silent failures.

### Automated emergency alerting
If any unhandled exception occurs at any point during Phase 1 or Phase 2:
- Full stack traces are captured and logged to disk, systemd journal, and SQLite.
- An emergency alert (`🚨 АВАРИЯ WB Agent: ...`) is immediately dispatched to Telegram, alerting developers and operators in seconds.

---

## Tech stack

| Layer | Technologies |
|---|---|
| **Core & Engine** | Python 3.10+, FastAPI, Pydantic Settings, Click CLI |
| **Marketplace API** | Wildberries Marketplace API v3, Content API v2, HTTPX (async client with throttling & backoff) |
| **Documents & Imaging** | Pillow, pypdf (PDF validation & inspection), python-barcode (Code128) |
| **Persistence** | SQLite with ACID transactions, thread locking, state tracking (`runs`, `run_events`, `supplies`) |
| **Distribution** | Telegram Bot API (resilient multipart document sender with retry loop) |
| **Infrastructure** | Linux VPS, systemd services & timers, logrotate, automated 30-day cleanup |

---

## Business impact

- **Zero manual assembly:** The entire morning supply collection and dispatch routine is 100% automated.
- **Eliminated fulfillment packing errors:** Pre-sorted stickers by article with framed separator tags reduced warehouse picking time by over 50%.
- **Zero deadline penalties:** Automated two-phase execution runs with second-level precision, eliminating late shipment fines.
- **Time saved:** Saves 1.5–2 hours of high-stress manual operational work every morning for the brand manager and warehouse staff.

---

## My role

Architect and AI Product Engineer. Conducted operational discovery with the client and warehouse manager, reverse-engineered marketplace logistics flows, implemented the Python backend, asynchronous API client, document generation engine, verification checks, and automated deployment on a Linux VPS.

---

## Public case-study boundary

Wildberries API tokens, client commercial credentials, seller secrets, and fulfillment Telegram group chat IDs are strictly private. This case study documents the workflow, architecture, and engineering solutions.
