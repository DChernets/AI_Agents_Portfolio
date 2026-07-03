# SENSOR - Telegram Intelligence Platform

**Production SaaS for Telegram lead generation, audience intelligence, source discovery, and conversational search.**  
Website: [sensor-tg.tech](https://sensor-tg.tech)  
Bot: [@sensor_tg_bot](https://t.me/sensor_tg_bot)

---

## Overview

SENSOR helps teams turn Telegram communities into a structured business signal system. It connects a user's Telegram account, monitors selected chats and channels, detects demand with AI, builds searchable knowledge bases, scores potential customers, and recommends new sources to monitor.

The product is built around five core modules: SENSOR.Leads, SENSOR.Chat, SENSOR.Audience, SENSOR.Catalog, and SENSOR.Tasks.

---

## Product Modules

### SENSOR.Leads
Lead monitoring and qualification from Telegram sources:
- semantic onboarding from a free-form business description;
- automatic generation of keywords, stopwords, and AI intent prompt;
- two processing modes: raw keyword monitoring and AI-qualified leads;
- live monitoring of Telegram groups/channels through userbot sessions;
- historical scans by natural-language period;
- hybrid recall: local keyword matching plus bounded Telegram search;
- context-aware AI evaluation of message chains, replies, and nearby messages;
- deduplication of repeated leads and repeated raw matches;
- lead delivery through Telegram bot and web dashboard;
- CSV export for leads and raw keyword matches.

### SENSOR.Chat
Conversational RAG over collected Telegram data:
- chat ingestion from selected Telegram sources;
- Gemini FileSearch / semantic retrieval over collected messages;
- source-aware answers with context;
- topic digest generation during ingest;
- overview-question handling from stored digest data;
- web and bot flows for starting and querying conversations.

### SENSOR.Audience
Audience intelligence for people already active in monitored communities:
- passive collection of active participants from project sources;
- audience history collection by thematic keywords or full selected chat sweep;
- audience account enrichment with public Telegram profile data;
- AI scoring per project: overall, interest, client fit, recency, and noise;
- verdicts: hot, promising, not fit, insufficient data;
- evidence quotes with links back to source messages;
- filtered audience lists, member cards, counters, and CSV export;
- safe outreach model: Telegram deep links only, no automated cold DMs.

### SENSOR.Catalog
Telegram source discovery and recommendations:
- organization-scoped source catalog for channels, megagroups, and chats;
- source profile enrichment with title, username, description, category, geo/language hints, and member count;
- Telegram similar-source recommendations through project userbot;
- source similarity edges from Telegram recommendations and audience overlap;
- source graph built from passive active-author overlap using salted hashes;
- "similar sources" view in bot and web dashboard;
- add recommended public sources through the existing autojoin/source flow;
- Pro+ limits for source discovery to control Telegram request risk.

### SENSOR.Tasks
Scheduled AI digests and recurring intelligence tasks:
- natural-language task creation through a semantic parser;
- scheduled digest generation from Telegram messages;
- AI summaries delivered back through the Telegram bot;
- safe Telegram HTML formatting for generated digests;
- task execution tracked through scheduler and storage models.

---

## Platform Features

- Multi-tenant organizations and team support
- QR / phone-code Telegram account connection
- Stable userbot profile binding for lead projects
- Fernet-encrypted Telegram session storage
- PostgreSQL-first storage with async SQLAlchemy
- FastAPI backend for the web dashboard
- React/Vite web dashboard at `app.sensor-tg.tech`
- Telegram bot management interface
- Billing tiers and quota gates
- YooKassa, CryptoPay, and Telegram Stars payment providers
- AI credit accounting for chat, history scans, audience scoring, and source discovery
- Cross-process job runners for long-running scans, collection, and scoring
- Persistent memory / AI context layer for better project-specific assistance
- Langfuse-ready LLM observability hooks

---

## Business Value

| Problem | SENSOR Solution |
|---------|-----------------|
| Manual Telegram monitoring misses buying intent | SENSOR.Leads detects demand continuously |
| Keyword alerts are noisy | AI mode evaluates context and conversation chains |
| Teams do not know which chats to monitor next | SENSOR.Catalog recommends similar sources |
| Community members are hard to qualify | SENSOR.Audience scores active participants with evidence |
| Chat history is hard to search | SENSOR.Chat turns Telegram history into a RAG knowledge base |
| Multiple clients need isolated data | Organizations, userbot profiles, and encrypted sessions isolate data |

---

## Target Users

- Web3 and crypto community managers
- Marketing and lead generation agencies
- Telegram marketplace owners
- Media buyers and growth teams
- B2B companies that sell through Telegram communities
- Teams that need searchable Telegram knowledge bases

---

## Tech Stack

| Area | Technology |
|------|------------|
| Backend | Python 3.10+/3.11, FastAPI, asyncio |
| Telegram | Telethon, Pyrogram, python-telegram-bot |
| AI | Google Gemini, google-genai, FileSearch/RAG |
| Database | PostgreSQL 16, async SQLAlchemy |
| Frontend | React, Vite, TypeScript |
| Billing | YooKassa, CryptoPay, Telegram Stars |
| Security | Fernet encrypted sessions, tenant-scoped access checks |
| Deployment | Docker Compose, nginx, Linux VPS, systemd-style ops |
| Observability | structured logs, LLM tracing hooks |

---

## Architecture

```text
Telegram user account
        |
        v
QR / phone auth -> encrypted session -> stable userbot profile
        |
        v
Collector / scanner layer
        |
        +--> SENSOR.Leads: matches, AI lead scoring, delivery, CSV
        |
        +--> SENSOR.Chat: ingest, FileSearch/RAG, digest, answers
        |
        +--> SENSOR.Audience: active member base, scoring, evidence, export
        |
        +--> SENSOR.Catalog: source catalog, recommendations, overlap graph
        |
        +--> SENSOR.Tasks: scheduled AI digests and recurring checks
        |
        v
Telegram bot + FastAPI web dashboard + billing/limits
```

---

## Status

| Area | Status |
|------|--------|
| Multi-tenant Telegram auth | Production |
| SENSOR.Leads live monitoring | Production |
| Keyword and AI processing modes | Production |
| Historical lead scans | Production |
| SENSOR.Chat RAG | Production |
| SENSOR.Audience scoring/export | Implemented |
| SENSOR.Catalog recommendations | Implemented |
| SENSOR.Tasks scheduled digests | Implemented |
| Web dashboard API | Implemented |
| Billing and plan limits | Implemented |
| Team / organization model | Implemented |

---

*Built with Python, Telegram APIs, Google Gemini, PostgreSQL, FastAPI, and React.*
