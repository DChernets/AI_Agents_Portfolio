# SENSOR - AI-Powered Telegram Intelligence Platform

**Production SaaS for Telegram lead generation and conversational search.**  
Website: [sensor-tg.tech](https://sensor-tg.tech)

---

## Overview

SENSOR turns Telegram chats and channels into a business intelligence system. It collects messages, analyzes commercial intent with AI, finds qualified leads, and builds searchable knowledge bases from Telegram history.

---

## Core Modules

### SENSOR.Leads
AI lead generation from Telegram communities:
- Monitors selected Telegram chats, groups, and channels
- Detects commercial demand with semantic AI analysis
- Scores lead quality and urgency
- Delivers qualified leads to a manager channel or bot interface
- Uses feedback calibration to improve future lead quality

### SENSOR.Chat
RAG search over Telegram message history:
- Collects and indexes chat history
- Enables natural-language questions over collected messages
- Returns answers with source context
- Works as a Telegram-specific knowledge base for communities and teams

### Multi-Tenant Account Layer
- Each user connects their own Telegram account
- QR code or phone-code authentication
- Encrypted session storage
- Tenant-level data isolation
- Separate monitored sources, chats, and lead projects per user

---

## Business Value

| Problem | SENSOR Solution |
|---------|-----------------|
| Manual monitoring misses customer intent | AI monitors Telegram discussions continuously |
| Keyword filters produce noisy results | Semantic analysis understands context and demand |
| Chat history is hard to search | RAG turns Telegram history into a queryable knowledge base |
| Teams need fast lead response | Qualified leads are delivered directly to managers |
| Multiple clients need isolated data | Multi-tenant architecture keeps sessions and data separated |

---

## Key Features

- Telegram group/channel monitoring
- AI-powered lead scoring
- Commercial intent detection
- RAG search with source context
- Userbot-based message collection
- Telegram bot management interface
- Feedback-based quality calibration
- Encrypted Telegram sessions
- Multi-tenant project structure
- Production-oriented billing and limits architecture

---

## Use Cases

- Web3 and crypto community lead generation
- Marketing agency prospect monitoring
- Telegram marketplace demand detection
- Community knowledge base search
- Competitor and market signal tracking
- Customer support search across historical discussions

---

## Tech Stack

| Component | Technology |
|-----------|------------|
| Language | Python 3.10+ |
| Backend | FastAPI, asyncio |
| Telegram clients | Telethon, Pyrogram |
| Bot layer | python-telegram-bot |
| AI | Google Gemini |
| RAG | FileSearch / semantic retrieval |
| Database | SQLite, PostgreSQL-ready architecture |
| Security | Fernet encrypted sessions |
| Deployment | Linux VPS, systemd |

---

## Architecture Highlights

```text
User Telegram Account
        |
        v
QR / Phone Auth -> Encrypted Session Storage
        |
        v
Collector Manager -> Message Store -> AI Analysis
        |                              |
        |                              +-> SENSOR.Leads scoring and delivery
        |                              |
        +------------------------------+-> SENSOR.Chat indexing and RAG search
```

---

## Status

| Area | Status |
|------|--------|
| Multi-tenant Telegram auth | Complete |
| Message collection | Complete |
| AI lead scoring | Complete |
| SENSOR.Chat RAG | Complete |
| Lead delivery | Complete |
| Feedback calibration | Complete |
| Billing and limits architecture | In progress |
| Security hardening | In progress |

---

*Built with Python, Telegram APIs, Google Gemini, and RAG tooling.*
