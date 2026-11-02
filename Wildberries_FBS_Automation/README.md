# Wildberries FBS Automation, Operations Dashboard & AI Review Agent

**Production system for a Wildberries seller: autonomous marketplace order processing, multi-warehouse supply grouping, sticker & QR document generation, fulfillment dispatch, a web operations dashboard, and a human-in-the-loop AI agent that drafts replies to customer reviews.**

Live in production since 16.10.2026 (FBS automation and dashboard). The AI review agent runs in semi-automatic mode since 29.10.2026: it only prepares drafts, and every reply is approved by an operator before it is sent.

Contents: [FBS automation](#delivered-workflow) · [Operations dashboard](#operations-dashboard) · [Review monitoring](#review-monitoring) · [AI review agent](#ai-review-agent)

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
- **Logistics Specialization:** Automatically allocates required transit cargo boxes (`trbx`) for pickup points (Koledino PVZ) while skipping redundant boxes for sort centers (SC).
- **Post-Step Verification:** Re-queries the WB API (`_verify_phase1`) to verify that 100% of orders are registered in the supplies, self-heals missing cargo boxes, and confirms zero uncollected orders remain in `orders/new`.
- **Status Broadcast:** Emits a structured morning summary to the fulfillment Telegram channel with warehouse order breakdowns.

### 2. Phase 2: Delivery Commit, Document Pipeline & Fulfillment (09:44 MSK)
- **Irreversible Commit:** Executes `PATCH /api/v3/supplies/{id}/deliver` across all supplies and downloads official WB barcodes.
- **Targeted Sticker Generation:** Compiles a unified multi-page PDF (`{DD.MM} стикеры.pdf`):
  - Orders are grouped by seller article.
  - Each product batch is preceded by a high-contrast separator label framed in 58×40 mm: **[Article name / N pcs]**.
  - Followed by exactly `N` official WB order QR stickers (58×40 mm).
- **Unified Supply QR PDF:** Generates `{DD.MM} поставки.pdf` containing one official 58×40 mm supply barcode per supply for warehouse intake scanning, plus the cargo-box (`trbx`) sticker for the Koledino pickup point, which the point does not accept without.
- **Inventory Write-off Export:** Compiles `{DD.MM} списание.txt`: a plain daily list of article totals (no per-city split) that the warehouse operator uses for manual write-off. MoySklad integration is a planned next stage, not part of the current system.
- **Document Integrity Auditing:** Uses `pypdf` to parse and validate every generated PDF before delivery, guaranteeing that page counts match `(N articles + M orders)` and supply counts.
- **Resilient Telegram Delivery:** Sends all files and summaries directly into the 3PL fulfillment group chat with automatic retries. A read timeout does not trigger a resend, so the group never receives duplicate files.
- **Automated Lifecycle & Retention:** Rotates logs daily and enforces a strict 30-day retention window: files older than 30 days in `logs/` and `data/documents/` as well as historical SQLite `run_events` are automatically purged.

---

## Operations dashboard

A FastAPI + SQLite web dashboard on the same VPS gives the brand owner and operators one view of the store:

- **Daily orders and revenue matrix** per product: photo, rating, article, FBS stock, price with and without the marketplace discount (SPP), per-day color scale, sparkline, daily average, buyout rate, and a pinned monthly total column.
- **Out-of-stock risk alert:** products with less than N days of FBS stock left are highlighted.
- **Month switcher and charts:** orders and revenue histogram, plus a separate tab with month-by-month totals.
- **Supplies tab:** download the generated PDF and TXT files, and run the create/deliver phases manually.
- **Access control:** every page and API call requires a login (scrypt password hashes, server-side sessions, lockout after repeated failures, cross-origin write protection) and all actions are written to an audit log.

---

## Review monitoring

A daily job (10:30 MSK) reads the top organic reviews of the 16 key product cards, skips pinned ones, and posts one report to the marketing Telegram group. Cards whose top reviews are not 5 stars are flagged so the team can push fresh positive reviews above them.

---

## AI review agent

A reply assistant for customer reviews on Wildberries, built around one rule: the model writes drafts, a human decides what is published.

```text
sync new unanswered reviews (every 10 min)
  -> router: classify the scenario into structured JSON (defect, shipping damage, expectation mismatch, rating mismatch, off-topic, toxic, safety, legal threat, ...)
  -> policy: scenario x stars x settings -> draft / human only
  -> generator: product fact card + similar past replies + store rules
  -> deterministic guardrails (regenerate once on failure, otherwise to a human)
  -> LLM critic that checks claims against the facts (1-4 star reviews)
  -> operator approves, edits, rewrites with a comment, or skips in the dashboard
  -> send: re-fetch the review, post the reply, verify the marketplace moderation status
```

- **Grounded in facts:** the model only uses a per-product fact card that an operator reviews and confirms in the dashboard; any edit removes the confirmation.
- **Guardrails in code:** no contacts or links, no payment or compensation promises, no requests to change or delete a rating, no accusations of the buyer, brand signature and length limits, no mention of AI, similarity check against recent replies to avoid template answers.
- **Dangerous cases never go to the model alone:** injuries, legal threats and profanity are routed to a human with an immediate Telegram alert. Review text is passed to the model strictly as data, with prompt-injection defenses and red-team tests.
- **Safe sending:** a row lock prevents double posting (the API does not validate IDs), the review is re-fetched before sending, and the moderation status of every posted reply is checked afterwards.
- **LLM budget guard:** all calls go through a usage ledger with session and weekly caps, so the shared subscription is never exhausted.
- **Evaluation:** a golden set of 299 real review cases, scored by an LLM judge and code checks. Latest full run (prompt v9): 100% of dangerous cases routed to a human, 0 negative reviews treated as positive, 0 unsafe drafts, 93.3% of drafts judged publishable, average judge score 4.79 out of 5, and 0 of 30 red-team prompts scoring 3 or lower.
- **Style:** replies are tuned to read like the store's own support, without typical AI markers (checked by code, 0 of 267 flagged in the last run).

Autopilot is intentionally not enabled; moving any scenario to automatic sending is a decision for the store owner.

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
| **Marketplace API** | Wildberries Marketplace API v3, Content API v2, Feedbacks API, HTTPX (async client with throttling & backoff) |
| **AI** | Ollama Cloud LLMs (generator, critic, judge), structured JSON routing, guardrails, evals harness |
| **Dashboard** | FastAPI, server-rendered HTML/JS, session auth, audit log |
| **Documents & Imaging** | Pillow, pypdf (PDF validation & inspection), python-barcode (Code128) |
| **Persistence** | SQLite with ACID transactions, thread locking, state tracking (`runs`, `run_events`, `supplies`, `orders_history`, `feedbacks`, users, sessions, audit log) |
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

Architect and AI Product Engineer. Conducted operational discovery with the client and warehouse manager, reverse-engineered marketplace logistics flows, implemented the Python backend, asynchronous API client, document generation engine, verification checks, operations dashboard, and automated deployment on a Linux VPS. Designed and built the AI review agent end to end: scenario taxonomy, prompts, guardrails, evaluation set and metrics, operator approval workflow. The codebase is covered by 1,385 automated tests.

---

## Public case-study boundary

Wildberries API tokens, client commercial credentials, seller secrets, and fulfillment Telegram group chat IDs are strictly private. This case study documents the workflow, architecture, and engineering solutions.
