# Dmitry Chernets — Applied AI Engineering Portfolio

Selected work in applied AI, Telegram intelligence, and document automation.

I build AI products end to end: from an ambiguous workflow problem and system design to backend implementation, integrations, deployment, and iteration with users. The projects below are production systems or active product work; source code is intentionally not published because it contains commercial logic, third-party integrations, and security-sensitive operational details.

Based in Bangkok and working remotely with international teams.

## Selected work

### [SENSOR — Telegram intelligence platform](./SENSOR/)

SENSOR started as a personal tool for navigating fast-moving crypto Telegram chats. I wanted a NotebookLM-like way to collect conversations, search them semantically, and return to the original source context instead of scrolling through chat history.

It grew into a production AI platform for Telegram intelligence, semantic monitoring, and lead generation. The product helps teams find relevant commercial conversations, research communities, and build searchable knowledge bases from the Telegram sources they follow.

**My role:** founder and applied AI engineer. I own product discovery, architecture, Python/FastAPI backend, Telegram integrations, LLM workflows, database design, security, billing, deployment, and iteration.

**Stack:** Python, FastAPI, PostgreSQL, Telethon, Pyrogram, Google Gemini, retrieval workflows, React/TypeScript, Docker, nginx.

[Product case study →](./SENSOR/)

---

### [Moqup — import and operations automation](./Moqup/)

Production services for import, logistics, and CRM workflows: AI-assisted TN VED classification, document generation, CRM-to-Excel exports with product images, a RAG-powered knowledge-base assistant (pgvector), and scheduled webhook automations.

**Stack:** Python, FastAPI, PostgreSQL, pgvector, Google Gemini, OpenPyXL, python-docx, systemd.

[Project details →](./Moqup/)

---

### [Cleaning Manager — tender document processing](./Cleaning_manager/)

Production workflow for processing incoming tender documents. It ingests files from Gmail and Google Drive, extracts requirements from office documents and scanned PDFs, and generates calculated Excel outputs for the operations team.

**Stack:** Python, Google Drive API, Gmail API, OCR, LLM extraction, OpenPyXL, PyMuPDF.

[Project details →](./Cleaning_manager/)

---

### [AI_SMM — content workflows for Telegram sellers](./AI_SMM/)

AI-assisted workflow for marketplace and wholesale sellers: product photos are enhanced, product information is turned into marketing content, and publications are scheduled to Telegram channels.

**Stack:** Python, Telegram Bot API, Google Gemini, PostgreSQL, Redis, Google Sheets API.

[Project details →](./AI_SMM/)

---

### [Industrial document intelligence](./industrial_automation/)

Active product direction for engineering and project teams. The implemented module analyzes tender documentation; the broader workflow for contracts, engineering documents, drawings, and structured project data remains in development.

**Stack:** Python, document parsing, OCR, LLM analysis, Excel/Word generation.

[Project details →](./industrial_automation/)

## What I work on

- LLM-powered workflows, agents, and retrieval/search systems
- Python backends, async APIs, PostgreSQL, and integrations
- Telegram, Google Workspace, CRM, and document-processing workflows
- Production concerns: access boundaries, user feedback loops, testing, deployment, and observability

## Contact

- LinkedIn: [Dmitry Chernets](https://www.linkedin.com/in/dmitry-chernets/)
- SENSOR: [sensor-tg.tech](https://sensor-tg.tech)
