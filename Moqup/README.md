# Moqup - Import and Logistics Automation Platform

**Business automation platform for China-to-Russia import, logistics, customs classification, CRM workflows, and document generation.**

---

## Overview

Moqup is a production microservice platform that automates operational workflows for an import and logistics business. It combines AI-assisted customs classification, broker responses, CRM data export, document generation, and scheduled webhook automation.

The platform is built as a set of independent services sharing common business entities and a PostgreSQL-first architecture.

---

## Microservices

### AI Broker API
Main AI service for product classification and broker guidance:
- Receives product data via webhook
- Performs Step 1: shortlist of TN VED codes and clarification questions
- Stores request state in PostgreSQL
- Accepts client clarifications
- Performs Step 2: final code selection, documents, risks, Chestny Znak checks, and recommendations
- Provides JSON API and development UI

### TNVED API
Legacy FastAPI service for customs classification:
- Determines 10-digit TN VED codes
- Calculates customs duty and VAT
- Supports product descriptions and optional images
- Sends results back to CRM or website postback endpoints

### CRM2Sheets
CRM export automation:
- Receives CRM webhooks
- Generates styled Excel files
- Embeds product images into spreadsheets
- Supports Google Sheets templates and downloadable outputs

### Doc Filler
Document generation service:
- Fills Word templates from structured order/client data
- Generates contracts, invoices, and shipment documents
- Runs as a webhook-driven FastAPI service

### Scheduler
Automation engine for recurring tasks:
- Scheduled webhook execution
- Configurable endpoints and timing
- systemd-managed production process

### Chatbot — AI Knowledge-Base Assistant
RAG-powered consultant for foreign trade, import, and customs operations:
- Answers questions about customs procedures, TN VED classification rules, and import compliance
- Retrieval-augmented generation over a knowledge base using **pgvector** for semantic search
- Embeds regulatory documents, guides, and reference materials into PostgreSQL with vector similarity matching
- Provides source-linked answers so users can verify the origin of each recommendation
- Handles multi-turn conversations with context awareness

### Product Search
Iframe-ready tool for personal accounts:
- Step-by-step brief collection for sourcing products in China
- Session-based draft storage
- AI-assisted summary and normalization
- Designed for web UI rather than Telegram-first interaction

---

## Architecture Highlights

- Microservice architecture with shared business context
- PostgreSQL as the main database
- pgvector for semantic search and RAG in the chatbot service
- Async-first FastAPI services
- Webhook-based integration with CRM and external websites
- systemd deployment on Linux VPS
- Environment-based configuration and protected endpoints

---

## Tech Stack

| Category | Technologies |
|----------|--------------|
| Backend | Python 3.10+, FastAPI, asyncio |
| Database | PostgreSQL, pgvector (RAG / semantic search) |
| AI | Google Gemini |
| Documents | openpyxl, Pillow, python-docx |
| Integrations | Webhooks, Google Sheets API |
| Deployment | Linux VPS, systemd, nginx |
| Validation | Pydantic |
| HTTP | httpx |

---

## Business Impact

- Reduced manual customs classification and broker response work
- Automated CRM-to-Excel exports with product images
- Standardized document generation from templates
- Created a shared foundation for future client memory, RAG, and CRM enrichment
- Centralized operational workflows into production-managed services

---

## Production Environment

Deployed on a dedicated Linux server with systemd-managed services:

```text
moqup-ai-broker
moqup-tnved
moqup-crm2sheets
moqup-docfiller
moqup-scheduler
moqup-chatbot
```

---

## Status

| Service | Status |
|---------|--------|
| AI Broker | Production / main AI API |
| TNVED API | Legacy production service |
| CRM2Sheets | Production |
| Doc Filler | Production |
| Scheduler | Production |
| Chatbot | Production (RAG with pgvector) |
| Product Search | Planned / architecture ready |

---

*Built with Python, FastAPI, PostgreSQL, Google Gemini, and document automation tooling.*
