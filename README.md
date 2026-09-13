# Dmitrii Chernets - Applied AI Engineering Portfolio

Selected production systems and active product work in applied AI, Telegram intelligence, and document automation.

I build AI products for businesses end to end: I clarify the workflow with users and domain experts, define the first useful version, implement the product, deploy it, and iterate from real feedback. The source code is private because these systems contain customer workflows, commercial logic, third-party integrations, and security-sensitive operational details.

## Selected work

### [SENSOR - Telegram intelligence platform](./SENSOR/)

Production multi-tenant platform for Telegram monitoring, semantic search, and commercial-demand discovery. Teams connect selected sources, review evidence-backed signals, search collected discussions with links to the original context, and improve relevance through feedback.

**My role:** founder and AI Product Engineer. I own product discovery, architecture, Python/FastAPI backend, React/TypeScript interface, Telegram integrations, LLM and retrieval workflows, security boundaries, billing, deployment, and iteration with users.

**Stack:** Python, FastAPI, PostgreSQL, Telethon, Pyrogram, Google Gemini, React/TypeScript, Docker, nginx.

[Product case study](./SENSOR/)

---

### [Import and operations automation](./Moqup/)

Production services for an import and logistics business: AI-assisted customs classification and broker guidance, CRM-to-Excel exports with product images, document generation, a RAG knowledge-base assistant backed by pgvector, and scheduled webhook automations.

**Stack:** Python, FastAPI, PostgreSQL, pgvector, Google Gemini, OpenPyXL, python-docx, Google Workspace APIs, systemd.

[Project details](./Moqup/)

---

### [Tender Manager for a cleaning company](./Cleaning_manager/)

Production workflow for a cleaning business. It monitors Gmail and Google Drive, processes office documents and scanned PDFs, extracts tender requirements, applies business calculations, and returns structured Excel outputs to the operations team.

**Stack:** Python, Google Drive API, Gmail API, OCR, LLM extraction, OpenPyXL, PyMuPDF.

[Project details](./Cleaning_manager/)

---

### [AI SMM - content workflow for wholesale suppliers](./AI_SMM/)

Active product for wholesale suppliers selling through Telegram. A supplier sends product photos; the system recognizes the product, improves the images, generates a product card, manages the catalogue, and schedules publication to connected channels.

**Stack:** Python, Telegram Bot API, Google Gemini, PostgreSQL, Redis, Google Sheets API.

[Project details](./AI_SMM/)

---

### [Industrial document intelligence](./industrial_automation/)

A native macOS document-intelligence application for an industrial gas-cleaning engineering company. Its tender-analysis module extracts requirements and missing inputs; its contract workflow compares clauses with the company's playbook, performs local redaction and LLM analysis, supports operator review, and generates a Word protocol. The application is being hardened for an internal pilot.

**Stack:** Python, document parsing, LLM analysis, local redaction, rules and precedents, Word generation, pywebview, macOS packaging.

[Project details](./industrial_automation/)

## How I work

- Product discovery, domain research, user workflows, and first-version scope
- AI-native implementation with Codex, Claude Code, and reusable agent instructions
- LLM applications, retrieval, structured outputs, evaluation, and feedback loops
- Python backends, PostgreSQL, web interfaces, integrations, and document pipelines
- Deployment, access boundaries, observability, support, and iteration with users

## Contact

- LinkedIn: [Dmitrii Chernets](https://www.linkedin.com/in/dmitry-chernets/)
- SENSOR: [sensor-tg.tech](https://sensor-tg.tech)
