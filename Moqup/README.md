# Import and Operations Automation

**Production services for an import and logistics business**

## Business context

The company handles product sourcing, customs classification, CRM records, documents, spreadsheets with product images, and recurring integrations. These workflows were implemented as a set of production services so each process could be deployed and supported independently.

## Delivered workflows

### AI customs broker

The service receives product information, proposes a shortlist of TN VED codes and clarification questions, stores the request state, and produces a structured final response with classification guidance, documents, risks, and related checks.

### CRM and spreadsheet automation

CRM webhooks trigger styled Excel exports with product information and embedded images. The workflow also supports Google Sheets templates and downloadable outputs.

### Document generation

Structured CRM and order data is applied to Word templates for business documents used by the operations team.

### Knowledge-base assistant

A production RAG assistant answers questions about import, customs, and operational procedures using the company's reference materials. It retrieves relevant passages through pgvector, provides links to the supporting sources, and maintains context across multi-turn conversations.

### Scheduled integrations

A small scheduling service executes recurring webhooks and integration tasks under production monitoring.

## Engineering approach

- independent FastAPI services with clear operational boundaries;
- PostgreSQL for persistent request and business state, with pgvector for semantic retrieval;
- asynchronous external API and webhook integrations;
- validation of structured model outputs before they enter downstream workflows;
- Linux deployment with systemd, nginx, logs, and service-level recovery.

## My role

I translated operating workflows into service boundaries, designed the APIs and data model, implemented the AI and document pipelines, integrated them with the company's CRM and Google workflows, and deployed and supported the services on a production server.

## Technology

Python, FastAPI, asyncio, PostgreSQL, pgvector, Google Gemini, OpenPyXL, python-docx, Google Sheets API, webhooks, httpx, Pydantic, Linux, systemd, and nginx.

## Public case-study boundary

The repository contains a case-study description only. Customer data, CRM schemas, credentials, business rules, and production source code are private.
