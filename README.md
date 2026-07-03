# AI Agents Portfolio

Portfolio of production AI agents and automation systems built with Python, FastAPI, Telegram, document processing, and LLM integrations.

---

## Projects

### [SENSOR](./SENSOR/)
AI-powered Telegram intelligence platform for lead generation and chat knowledge bases.

SENSOR monitors Telegram groups, detects commercial intent with AI, and turns collected messages into searchable RAG knowledge bases.

**Features:**
- Multi-tenant Telegram account connection via QR code or phone login
- AI lead detection from Telegram chats, channels, and communities
- Semantic analysis beyond keyword matching
- SENSOR.Chat: conversational RAG search over collected Telegram messages
- SENSOR.Leads: lead scoring, manager delivery, and feedback calibration
- Encrypted Telegram session storage and tenant data isolation

**Technologies:** Python, FastAPI, Telethon, Pyrogram, python-telegram-bot, Google Gemini, FileSearch/RAG, SQLite/PostgreSQL

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
- **Projects with document automation:** 4
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

---

## Contacts

- GitHub: [@DChernets](https://github.com/DChernets)

---

*Portfolio updated regularly*
