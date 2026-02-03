# TG Krot - Telegram Lead Generation Bot

Система для автоматического сбора лидов из Telegram чатов с использованием Gemini AI для фильтрации.

## Архитектура

```
┌─────────────────┐     ┌──────────────┐     ┌─────────────────┐
│ Collector Layer │────▶│ Filter Layer │────▶│ Delivery Layer  │
│  (Pyrogram)     │     │ (Gemini AI)  │     │  (BotFather)    │
└─────────────────┘     └──────────────┘     └─────────────────┘
        ↓                       ↓                       ↓
  Public Groups          Quality Scoring         Manager Channel
  (10-50 chats)         (0.0 - 1.0 score)        (Qualified leads)
        ↓                       ↓                       ↓
  SQLite DB              Extracted Data           Delivery Log
```

## Установка

### 1. Клонирование и зависимости

```bash
cd /Users/rocksteady/myAI/TG_Krot
pip install -r requirements.txt
```

### 2. Настройка переменных окружения

Скопируйте `.env.example` в `.env` и заполните:

```bash
cp .env.example .env
```

Обязательные переменные:
- `TG_API_ID` - получить на https://my.telegram.org
- `TG_API_HASH` - получить на https://my.telegram.org
- `TG_PHONE` - номер телефона для userbot (аккаунт с "отлежкой")
- `BOT_TOKEN` - токен от @BotFather
- `MANAGER_CHANNEL_ID` - ID канала для лидов (например: -1001234567890)
- `ADMIN_IDS` - ID администраторов через запятую
- `GEMINI_API_KEY` - ключ от https://makersuite.google.com/app/apikey

### 3. Инициализация базы данных

```bash
python scripts/init_db.py
```

## Использование

### Запуск

```bash
python src/main.py
```

### Команды бота

- `/start` - Главное меню
- `/stats` - Статистика
- `/keywords` - Управление ключевыми словами
- `/groups` - Управление группами

## Структура проекта

```
TG_Krot/
├── .env                          # Конфигурация
├── requirements.txt              # Зависимости
├── config/
│   └── settings.py               # Настройки (Pydantic)
├── src/
│   ├── main.py                   # Точка входа
│   ├── storage/
│   │   ├── database.py           # База данных
│   │   └── models.py             # SQLAlchemy модели
│   ├── collector/
│   │   └── userbot.py            # Pyrogram userbot
│   ├── filter/
│   │   ├── ai_filter.py          # Gemini AI фильтр
│   │   └── rules.py              # Базовые правила
│   ├── delivery/
│   │   └── bot.py                # Telegram бот
│   └── management/
│       ├── menu_handlers.py      # Инлайн-меню
│       └── telegram_helpers.py   # Хелперы
└── scripts/
    └── init_db.py                # Инициализация БД
```

## Добавление групп для мониторинга

### Способ 1: Через бота

1. Отправьте `/groups`
2. Нажмите "➕ Добавить группу"
3. Отправьте ссылку или юзернейм группы
4. Вступите в группу с аккаунтом userbot'а
5. Получите chat_id через @getidsbot
6. Обновите в базе данных

### Способ 2: Напрямую в БД

```sql
INSERT INTO monitored_groups (chat_id, title, username, invite_link, is_active)
VALUES (-1001234567890, 'Название группы', 'username', 'https://t.me/joinchat/...', true);
```

## Добавление ключевых слов

Через бота:
1. Отправьте `/keywords`
2. Нажмите "➕ Добавить ключевое слово"
3. Введите слово или фразу

## Формат лида в канале

```
🔥 **НОВЫЙ ЛИД** [8.5/10]

👤 **От:** Иван Иванов (@username)
📍 **Чат:** Китайские товары
🔗 **Ссылка:** [message link]

💬 **Текст:**
Ищу поставщика электроники...

📊 **AI Анализ:**
- Срочность: 🔴 Высокая
- Бюджет: $5000-10000

📞 **Контакты:**
- Телефон: +7...

[✅ Связаться] [📁 Архивировать] [🚫 Спам]
```

## Стоимость Gemini API

- gemini-2.5-flash: ~$0.30 за 1M токенов (input)
- Примерный анализ 1 лида: ~500 токенов
- Стоимость 1 лида: ~$0.00015 (0.15₽)

## Масштабирование

Для 50+ чатов:
- SQLite → PostgreSQL
- Добавить Redis для очередей
- Несколько worker'ов

## Поиск проблем

```bash
# Проверка логов
tail -f logs/tg_krot.log

# Тест Gemini API
python -c "from src.filter.ai_filter import initialize_gemini_filter; import asyncio; asyncio.run(initialize_gemini_filter())"
```

## Лицензия

MIT
