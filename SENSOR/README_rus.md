# SENSOR - Telegram Intelligence Platform

**Production SaaS для лидогенерации, анализа аудитории, подбора Telegram-источников и диалогового поиска.**  
Сайт: [sensor-tg.tech](https://sensor-tg.tech)  
Бот: [@sensor_tg_bot](https://t.me/sensor_tg_bot)

---

## Обзор

SENSOR помогает превращать Telegram-сообщества в систему бизнес-сигналов: подключает Telegram-аккаунт пользователя, мониторит выбранные чаты и каналы, находит коммерческий спрос, строит поисковые базы знаний, оценивает потенциальных клиентов и рекомендует новые источники для мониторинга.

Продукт состоит из пяти основных модулей: SENSOR.Leads, SENSOR.Chat, SENSOR.Audience, SENSOR.Catalog и SENSOR.Tasks.

---

## Модули продукта

### SENSOR.Leads
Мониторинг и квалификация лидов из Telegram-источников:
- semantic onboarding из свободного описания бизнеса;
- автоматическая генерация keywords, stopwords и AI intent prompt;
- два режима обработки: raw keyword monitoring и AI-qualified leads;
- live-мониторинг Telegram-групп и каналов через userbot-сессии;
- исторические сканы за период, заданный естественным языком;
- hybrid recall: локальный keyword matching плюс ограниченный Telegram search;
- AI-оценка цепочек сообщений, reply-контекста и соседних сообщений;
- dedupe повторных лидов и raw keyword matches;
- доставка лидов через Telegram bot и web dashboard;
- CSV export для лидов и raw keyword matches.

### SENSOR.Chat
Диалоговый RAG по собранным Telegram-данным:
- ingest сообщений из выбранных Telegram-источников;
- Gemini FileSearch / semantic retrieval по собранной истории;
- ответы с контекстом источников;
- topic digest при индексации чата;
- ответы на overview-вопросы из сохраненного digest;
- bot и web flows для создания и использования чатов.

### SENSOR.Audience
Анализ аудитории, которая уже активна в отслеживаемых сообществах:
- пассивный сбор активных участников из источников проекта;
- broad history collection по тематическим словам или полному выбранному чату;
- обогащение аккаунтов публичными Telegram-данными;
- AI scoring под конкретный проект: overall, interest, client fit, recency, noise;
- verdicts: hot, promising, not fit, insufficient data;
- evidence quotes со ссылками на исходные сообщения;
- фильтры, карточки участников, счетчики и CSV export;
- безопасная outreach-модель: только Telegram deep links, без автоматических cold DM.

### SENSOR.Catalog
Подбор Telegram-источников и рекомендации:
- organization-scoped catalog каналов, мегагрупп и чатов;
- обогащение источников: title, username, description, category, geo/language hints, member count;
- Telegram similar-source recommendations через userbot проекта;
- source similarity edges по Telegram recommendations и audience overlap;
- source graph по пересечению активных авторов с salted hashes;
- экран похожих источников в bot и web dashboard;
- добавление рекомендованных public sources через существующий autojoin/source flow;
- Pro+ лимиты source discovery для контроля Telegram request risk.

### SENSOR.Tasks
Scheduled AI digests и повторяющиеся intelligence-задачи:
- создание задач естественным языком через semantic parser;
- генерация scheduled digest по Telegram-сообщениям;
- доставка AI-summary обратно через Telegram bot;
- безопасное Telegram HTML formatting для digest;
- выполнение задач через scheduler и storage models.

---

## Платформенные возможности

- multi-tenant organizations и team support;
- подключение Telegram-аккаунта через QR или phone code;
- stable userbot profile binding для lead-проектов;
- Fernet-encrypted Telegram session storage;
- PostgreSQL-first storage и async SQLAlchemy;
- FastAPI backend для web dashboard;
- React/Vite web dashboard на `app.sensor-tg.tech`;
- Telegram bot management interface;
- billing tiers и quota gates;
- YooKassa, CryptoPay и Telegram Stars payments;
- AI credit accounting для chat, history scans, audience scoring и source discovery;
- cross-process job runners для долгих scans, collection и scoring;
- persistent memory / AI context layer для более точной помощи внутри проекта;
- Langfuse-ready LLM observability hooks.

---

## Бизнес-ценность

| Проблема | Решение SENSOR |
|----------|----------------|
| Ручной мониторинг Telegram пропускает спрос | SENSOR.Leads постоянно ищет buying intent |
| Keyword alerts дают много шума | AI mode оценивает контекст и цепочки сообщений |
| Непонятно, какие чаты мониторить дальше | SENSOR.Catalog рекомендует похожие источники |
| Сложно понять, кто из аудитории потенциальный клиент | SENSOR.Audience скорит участников с evidence |
| Историю чатов трудно искать | SENSOR.Chat превращает Telegram history в RAG-базу знаний |
| У разных клиентов должны быть изолированные данные | Organizations, userbot profiles и encrypted sessions разделяют данные |

---

## Целевые пользователи

- Web3 и crypto community managers;
- маркетинговые и lead generation агентства;
- владельцы Telegram-маркетплейсов;
- media buyers и growth teams;
- B2B-компании, продающие через Telegram-сообщества;
- команды, которым нужна searchable база знаний по Telegram.

---

## Технологический стек

| Область | Технологии |
|---------|------------|
| Backend | Python 3.10+/3.11, FastAPI, asyncio |
| Telegram | Telethon, Pyrogram, python-telegram-bot |
| AI | Google Gemini, google-genai, FileSearch/RAG |
| Database | PostgreSQL 16, async SQLAlchemy |
| Frontend | React, Vite, TypeScript |
| Billing | YooKassa, CryptoPay, Telegram Stars |
| Security | Fernet encrypted sessions, tenant-scoped access checks |
| Deployment | Docker Compose, nginx, Linux VPS |
| Observability | structured logs, LLM tracing hooks |

---

## Архитектура

```text
Telegram account пользователя
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

## Статус

| Область | Статус |
|---------|--------|
| Multi-tenant Telegram auth | Production |
| SENSOR.Leads live monitoring | Production |
| Keyword and AI processing modes | Production |
| Historical lead scans | Production |
| SENSOR.Chat RAG | Production |
| SENSOR.Audience scoring/export | Реализовано |
| SENSOR.Catalog recommendations | Реализовано |
| SENSOR.Tasks scheduled digests | Реализовано |
| Web dashboard API | Реализовано |
| Billing and plan limits | Реализовано |
| Team / organization model | Реализовано |

---

*Создано на Python, Telegram APIs, Google Gemini, PostgreSQL, FastAPI и React.*
