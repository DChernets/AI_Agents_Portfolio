# Moqup - платформа автоматизации импорта и логистики

**Business automation platform для импорта из Китая в РФ, логистики, классификации ТН ВЭД, CRM-процессов и генерации документов.**

---

## Обзор

Moqup - production microservice-платформа, которая автоматизирует операционные процессы импортно-логистического бизнеса: AI-классификацию товаров, брокерские ответы, экспорт данных из CRM, генерацию документов и плановые webhook-задачи.

Платформа построена как набор независимых сервисов с общей бизнес-моделью и PostgreSQL-first архитектурой.

---

## Микросервисы

### AI Broker API
Основной AI-сервис для классификации товаров и брокерских рекомендаций:
- принимает данные товара по webhook;
- выполняет Step 1: shortlist кодов ТН ВЭД и уточняющие вопросы;
- сохраняет состояние заявки в PostgreSQL;
- принимает ответы клиента на уточнения;
- выполняет Step 2: финальный код, документы, риски, Честный Знак и рекомендации;
- предоставляет JSON API и dev UI.

### TNVED API
Legacy FastAPI-сервис для таможенной классификации:
- определяет 10-значный код ТН ВЭД;
- рассчитывает пошлину и НДС;
- поддерживает описание товара и опциональное изображение;
- отправляет результат обратно в CRM или postback внешнего сайта.

### CRM2Sheets
Автоматизация выгрузки CRM:
- принимает CRM webhooks;
- генерирует оформленные Excel-файлы;
- вставляет изображения товаров в таблицы;
- поддерживает Google Sheets templates и downloadable outputs.

### Doc Filler
Сервис генерации документов:
- заполняет Word-шаблоны структурированными данными заказа/клиента;
- генерирует договоры, счета и отгрузочные документы;
- работает как webhook-driven FastAPI сервис.

### Scheduler
Планировщик автоматизаций:
- выполняет webhook-задачи по расписанию;
- поддерживает настраиваемые endpoints и время запуска;
- работает в production через systemd.

### Product Search
Iframe-ready инструмент для личного кабинета:
- пошагово собирает бриф на поиск товара в Китае;
- сохраняет черновики по session_id;
- использует AI для summary и нормализации описаний;
- проектируется как web UI, а не Telegram-first сценарий.

---

## Архитектура

- microservice architecture с общим бизнес-контекстом;
- PostgreSQL как основная база данных;
- pgvector-ready дизайн для будущего semantic search;
- async-first FastAPI services;
- webhook-интеграции с CRM и внешними сайтами;
- production deployment через systemd на Linux VPS;
- environment-based конфигурация и защищенные endpoints.

---

## Технологический стек

| Категория | Технологии |
|-----------|------------|
| Backend | Python 3.10+, FastAPI, asyncio |
| Database | PostgreSQL, pgvector-ready architecture |
| AI | Google Gemini |
| Documents | openpyxl, Pillow, python-docx |
| Integrations | Webhooks, Google Sheets API |
| Deployment | Linux VPS, systemd, nginx |
| Validation | Pydantic |
| HTTP | httpx |

---

## Бизнес-эффект

- сокращение ручной работы по классификации товаров и брокерским ответам;
- автоматизация CRM-to-Excel выгрузок с изображениями товаров;
- стандартизация генерации документов по шаблонам;
- единая основа для будущей client memory, RAG и CRM enrichment;
- перенос ключевых операций в production-managed сервисы.

---

## Production

Сервисы развернуты на выделенном Linux-сервере и управляются через systemd:

```text
moqup-ai-broker
moqup-tnved
moqup-crm2sheets
moqup-docfiller
moqup-scheduler
moqup-chatbot
```

---

## Статус

| Сервис | Статус |
|--------|--------|
| AI Broker | Production / основной AI API |
| TNVED API | Legacy production service |
| CRM2Sheets | Production |
| Doc Filler | Production |
| Scheduler | Production |
| Chatbot | В разработке |
| Product Search | Запланирован / архитектура готова |

---

*Создано на Python, FastAPI, PostgreSQL, Google Gemini и инструментах document automation.*
