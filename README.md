# AI Agents Portfolio

Portfolio of production AI agents and automation systems built with Python, FastAPI, Telegram, document processing, and LLM integrations.

---

## Projects

### [SENSOR](./SENSOR/)
Telegram intelligence SaaS for lead generation, audience analysis, source discovery, and conversational search.

SENSOR connects a user's Telegram account, monitors selected chats and channels, detects buying intent, scores active audience members, recommends new Telegram sources, and turns collected messages into searchable RAG knowledge bases.

**Features:**
- SENSOR.Leads: keyword and AI modes, live monitoring, historical scans, lead delivery, CSV export
- SENSOR.Chat: Telegram message ingest, FileSearch/RAG, topic digest, source-aware answers
- SENSOR.Audience: active participant collection, AI scoring, evidence quotes, CSV export
- SENSOR.Catalog: source catalog, similar-source recommendations, audience-overlap graph
- SENSOR.Tasks: scheduled AI digests and recurring Telegram intelligence tasks
- Multi-tenant organizations, team support, encrypted Telegram sessions, stable userbot profiles
- Web dashboard, Telegram bot UI, billing tiers, quotas, YooKassa/CryptoPay/Telegram Stars

**Technologies:** Python, FastAPI, PostgreSQL, Telethon, Pyrogram, python-telegram-bot, Google Gemini, FileSearch/RAG, React/Vite, Docker, nginx

---

### [AI_SMM](./AI_SMM/)
Telegram bots for wholesale suppliers and marketplace sellers.

Automated product catalog management and Telegram channel publishing using AI.

**Features:**
- AI product recognition from photos
- Automatic photo and text enhancement
- Scheduled publishing to Telegram channels
- Price list and informational post automation
- AI-powered support bot

**Technologies:** Python, Telegram Bot API, Google Gemini, PostgreSQL, Redis, Google Sheets API

---

### [Moqup](./Moqup/)
Business automation platform for import, logistics, and CRM workflows.

Microservice platform for China-to-Russia import operations: product classification, broker responses, document generation, CRM exports, and scheduled automations.

**Features:**
- AI Broker API for two-step TN VED classification and customs guidance
- Legacy TNVED API for customs code and duty calculation
- CRM2Sheets export from CRM webhooks to Excel with product images
- Doc Filler for contracts, invoices, and shipping documents
- Shared PostgreSQL database with pgvector-ready architecture
- Scheduler for webhook automation

**Technologies:** Python, FastAPI, PostgreSQL, pgvector, Google Gemini, openpyxl, python-docx, systemd

---

### [Cleaning_manager](./Cleaning_manager/)
Cleaning tender processor with Google Drive and AI document analysis.

Production system that monitors incoming tender documents, extracts data, analyzes requirements, and generates calculated Excel outputs.

**Features:**
- Google Drive and Gmail document ingestion
- Support for DOCX, DOC, PDF, XLS, XLSX
- OCR for scanned PDFs
- AI extraction via Polza.ai
- Excel generation with regional and population coefficients
- Duplicate-safe continuous processing

**Technologies:** Python, Google Drive API, Gmail API, Polza.ai, Tesseract OCR, OpenPyXL, PyMuPDF

---

### [industrial_automation](./industrial_automation/)
Industrial document automation for engineering and project teams.

AI-assisted system for contract review and cross-document validation in industrial engineering projects.

**Features:**
- Contract review against internal templates and risk rules
- Protocol of disagreements generation for customer contracts
- Validation of project documentation across PDF, DOCX, XLSX, and DWG-derived data
- Cross-checking KKS codes, cables, signals, equipment, specifications, and revisions
- Source data completeness checks and project document registry
- Human approval workflow for legal and engineering decisions

**Technologies:** Python, document parsing, OCR, LLM analysis, Excel/Word generation, rules engine, CAD/PDF processing pipeline

---

## Statistics

- **Total Projects:** 5
- **Production Projects:** 4
- **Projects with Telegram Bot API:** 3
- **Projects with Google Gemini AI:** 3
- **Projects with document automation:** 3
- **Projects with FastAPI:** 2

---

## Key Technologies

| Technology | Projects |
|------------|----------|
| **Python** | All |
| **FastAPI** | Moqup, SENSOR |
| **Telegram Bot API** | SENSOR, AI_SMM, Moqup |
| **Google Gemini AI** | SENSOR, AI_SMM, Moqup |
| **PostgreSQL** | AI_SMM, Moqup, SENSOR |
| **Google Sheets API** | AI_SMM, Moqup, Cleaning_manager |
| **Google Drive API** | Cleaning_manager |
| **OCR / document parsing** | Cleaning_manager, industrial_automation |
| **RAG / semantic search** | SENSOR, Moqup |
| **React / Vite** | SENSOR |

---

## Contacts

- GitHub: [@DChernets](https://github.com/DChernets)

---

*Portfolio updated regularly*
