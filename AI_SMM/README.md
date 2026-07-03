# AI_SMM - Telegram Bots for Wholesale Suppliers

> Automate product catalog management and Telegram channel publishing with AI

## About

**AI_SMM** is a comprehensive automation solution for wholesale suppliers at marketplaces. The system consists of two integrated Telegram bots powered by Google Gemini AI:

**[@iaismm_bot](https://t.me/iaismm_bot)** - Main automation bot:
- AI product recognition from photos (Gemini 2.5 Flash)
- Automatic photo enhancement and marketing text generation
- Smart scheduling and auto-publishing to multiple channels
- Price list management and informative content generation

**[@aismm_support_bot](https://t.me/aismm_support_bot)** - AI-powered support:
- Automatic answers from knowledge base
- AI ticket classification (bug/feature/question)
- Screenshot handling for issue resolution

## Key Features

**AI Product Recognition:** Send product photo → AI extracts name, description, material, dimensions, packaging. Supports up to 10 photos per batch.

**Content Enhancement:** Professional backgrounds, quality processing, marketing copywriting — all automated via Gemini 2.5 Flash.

**Smart Publishing:**
- Automatic FIFO queue distribution across morning/evening windows
- Manual scheduling with calendar and time picker
- Multi-channel support with custom descriptions

**Informative Posts:** Auto-generated daily content — currency rates (USD, EUR, CNY, TRY), crypto, business news, supplier tips.

**Privacy-First:** Contact data (phones, addresses) added locally only — never sent to external APIs.

## Tech Stack

| Component | Technology |
|-----------|------------|
| Language | Python 3.9+ |
| Framework | python-telegram-bot 21.0+ with APScheduler |
| Database | PostgreSQL 15+ with pgvector, Redis |
| AI | Google Gemini 2.5 Flash (recognition + content) |
| APIs | Google Sheets/Drive, RSS feeds |
| Payments | YooKassa integration |
| Deployment | systemd services, VPS |

## Architecture Highlights

- **Dual-mode data layer:** PostgreSQL with Redis caching (with Google Sheets legacy fallback)
- **Slot-based scheduling:** Smart publication windows with conflict resolution
- **Multi-tenant:** Team functionality with role-based permissions
- **Atomic rate limiting:** Redis counters with auto-expiry per user
- **Async-first:** SQLAlchemy 2.0 async with connection pooling

## Business Model

| Plan | Product Posts | Info Posts | Features |
|------|--------------|------------|----------|
| FREE | 5/day | 1/day | AI recognition, basic features |
| START | 20/day | 3/day | Auto-publishing, full features |

7-day free trial for new users. Limits reset daily at 00:01 MSK.

## Results

- Fully automated daily content pipeline for supplier channels
- Reduced content creation time from hours to minutes
- 24/7 AI-powered support with automatic ticket classification
- Scalable multi-user architecture supporting team workflows

---

**Live Demo:** [@iaismm_bot](https://t.me/iaismm_bot) 

**© 2025 AI_SMM. Powered by Google Gemini AI.**
