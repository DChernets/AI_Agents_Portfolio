# AI_SMM - Telegram боты для оптовых поставщиков

> Автоматизация каталога товаров и публикаций в Telegram каналы с помощью AI

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/)
[![Telegram Bot](https://img.shields.io/badge/Telegram-Bot-blue.svg)](https://telegram.org/)
[![AI Powered](https://img.shields.io/badge/AI-Gemini%202.5-orange.svg)](https://ai.google.dev/)

**Боты:**
- 🤖 [@iaismm_bot](https://t.me/iaismm_bot) - основной бот
- 💬 [@aismm_support_bot](https://t.me/aismm_support_bot) - техподдержка

---

## 📋 О проекте

**AI_SMM** - это комплексное решение для оптовых поставщиков на рынках, которое помогает:
- Управлять каталогом товаров с AI-распознаванием фотографий
- Автоматически публиковать товары в Telegram каналы
- Улучшать фотографии и описания товаров с помощью Google Gemini
- Планировать публикации по расписанию
- Генерировать информационные посты (курсы валют, новости, советы)

### Два бота в одном проекте

**[@iaismm_bot](https://t.me/iaismm_bot)** - основной бот для работы
- Распознавание товаров по фото (AI Gemini 2.5 Flash)
- Улучшение фотографий и текстов
- Автоматическая публикация в каналы
- Управление прайс-листами
- Информационные посты

**[@aismm_support_bot](https://t.me/aismm_support_bot)** - техническая поддержка
- Автоматические ответы на вопросы (база знаний)
- Создание обращений в поддержку
- AI-ассистент для решения проблем
- Интеграция с основным ботом

---

## 🚀 Быстрый старт

### Для поставщиков

1. **Откройте бота** [@iaismm_bot](https://t.me/iaismm_bot)
2. **Нажмите `/start`** для регистрации
3. **Заполните профиль:**
   - Ваше имя
   - Название рынка (например, "Садовод")
   - Номер павильона
   - Контактный телефон
4. **Добавьте Telegram канал** через кнопку 📺 ИЗМЕНИТЬ КАНАЛ
5. **Загрузите первый товар** через кнопку 📸 ДОБАВИТЬ НОВЫЙ ТОВАР

Готово! Вы получаете **бесплатный тариф FREE** с 5 публикациями товаров и 1 информационным постом в день.

---

## ✨ Возможности AI_SMM

### 📸 AI-распознавание товаров
- Отправьте фото товара - AI автоматически распознает:
  - Название товара
  - Описание
  - Материал
  - Размеры/объём
  - Информацию об упаковке
- Поддержка до 10 фото за раз
- Редактирование распознанных данных

### 🎨 Улучшение контента с помощью AI
- **Улучшенные фото:** профессиональные фоны, качественная обработка
- **Маркетинговые тексты:** продающие описания для публикаций
- Выбор между оригиналом и улучшенным контентом

### 📅 Публикация в каналы
**Автоматическая публикация:**
- Умное распределение постов по времени
- Утренние и вечерние окна публикаций
- FIFO очередь товаров

**Ручная публикация:**
- Выбор точной даты и времени
- Календарь и time picker
- Публикация в несколько каналов

### 💰 Прайс-листы
- Загрузка PDF, фото или Google Sheets
- Автоматическая публикация по расписанию
- Управление несколькими прайс-листами

### 💬 Информационные посты
Автоматическая генерация:
- 💵 Курсы валют (USD, EUR, CNY, TRY)
- ₿ Криптовалюты (Bitcoin, Ethereum)
- 📰 Новости для бизнеса (VC.ru)
- 💡 Советы для поставщиков
- 📊 Итоги дня

### 📺 Управление каналами
- Добавление нескольких каналов
- Кастомные описания для каждого канала
- Публикация в выбранные каналы

### 🔐 Приватность
Все контактные данные (телефоны, адреса) добавляются **только локально** и никогда не отправляются на внешние API.

---

## 💬 Возможности Support Bot

**[@aismm_support_bot](https://t.me/aismm_support_bot)** - ваш помощник 24/7

### Основные функции
- ❓ **Автоматические ответы** из базы знаний
- 📝 **Создание обращений** через `/new`
- 📋 **Просмотр тикетов** через `/my_tickets`
- 📚 **FAQ** через `/faq`
- 🤖 **AI-классификация** проблем (bug/feature/question)

### Как работает
1. Задайте вопрос боту (просто напишите текст)
2. AI ищет ответ в базе знаний
3. Если не находит - создается тикет и уведомляется оператор
4. Можете приложить скриншоты для лучшего понимания

---

## 💎 Тарифные планы

| Тариф | Товарные посты/день | Информ. посты/день | Особенности |
|-------|--------------------:|-------------------:|-------------|
| **FREE** | 5 | 1 | AI-распознавание, базовые функции |
| **START** | 20 | 3 | AI-распознавание, авто-публикация |

**💡 Важно:** Информационные посты **НЕ входят** в лимит товарных постов!
- FREE: 5 товаров + 1 информативный = **6 постов в день**
- START: 20 товаров + 3 информативных = **23 постов в день**

Лимиты обновляются каждый день в **00:01 МСК**.

---

## 📖 Как пользоваться

### Добавить товар
Нажмите **📸 ДОБАВИТЬ НОВЫЙ ТОВАР** → отправьте фото → AI распознает товар → выберите локацию → сохраните. Готово!

### Опубликовать пост
**📦 МОИ ТОВАРЫ** → выберите товар → **📅 Публикация** → выберите канал, дату и время → подтвердите.

### Настроить автопубликацию
В карточке товара включите опцию "Автоматическое расписание". Бот будет публиковать товары автоматически каждый день.

### Загрузить прайс-лист
**📊 ПРАЙС-ЛИСТ** → **➕ Добавить** → выберите файл (PDF/фото) или ссылку на Google Sheets → выберите канал → установите время публикации.

### Получить помощь
Напишите боту [@aismm_support_bot](https://t.me/aismm_support_bot) - AI ответит автоматически или создаст тикет для оператора.

**📖 Полная документация:** [Руководство пользователя](docs/USER_GUIDE.md)

---

## ❓ Часто задаваемые вопросы

### Как начать пользоваться ботом?
Откройте [@iaismm_bot](https://t.me/iaismm_bot) и нажмите `/start`. Следуйте инструкциям для регистрации.

### Почему бот не публикует в моём канале?
1. Проверьте, что бот является **администратором** канала
2. Убедитесь что канал добавлен через `/channels`
3. Проверьте дневные лимиты публикаций в профиле

### Как работают улучшения фото?
AI (Gemini 2.5 Flash) создаёт профессиональное фото товара: убирает фон, добавляет красивый студийный фон, улучшает освещение и качество.

### Что такое информативные посты?
Автоматически генерируемые посты с курсами валют, крипты, новостями бизнеса и советами для поставщиков. Привлекают внимание подписчиков и повышают активность канала.

### Хватит ли мне лимитов на START тарифе?
START тариф (20 товаров + 3 инфо-поста в день) подходит для активной работы. Для расширенных возможностей обратитесь к администратору.

**📚 Полный FAQ:** [docs/USER_GUIDE.md](docs/USER_GUIDE.md#часто-задаваемые-вопросы)

---

## 💬 Техническая поддержка

**Возникли вопросы или проблемы?**

- 🤖 Бот поддержки: [@aismm_support_bot](https://t.me/aismm_support_bot)
- 📸 При описании проблемы приложите скриншоты
- 📖 Документация: [docs/USER_GUIDE.md](docs/USER_GUIDE.md)

**Мы отвечаем в порядке очереди!**

---
---

## 🔧 Для администраторов

> ⚠️ Этот раздел для разработчиков и системных администраторов, которые разворачивают ботов на сервере.

### Требования

- Python 3.9+
- Google Sheets API
- Google Drive API
- Google Gemini API
- Telegram Bot Tokens

### Установка

```bash
# Клонируйте репозиторий
git clone <repository-url>
cd AI_SMM

# Установите зависимости
pip install -r requirements.txt
```

### Настройка

1. **Создайте `.env` файл** на основе `.env.example`:

```bash
# Telegram Bot Tokens
TELEGRAM_BOT_TOKEN=your_bot_token_here           # Основной бот
SUPPORT_BOT_TOKEN=your_support_bot_token_here   # Support бот

# Google Sheets API
GOOGLE_SHEETS_CREDENTIALS_FILE=config/google_credentials.json
GOOGLE_SHEETS_SPREADSHEET_ID=your_spreadsheet_id_here
MARKET_SUPPORT_SPREADSHEET_ID=your_support_spreadsheet_id_here

# Google Gemini API
GEMINI_API_KEY=your_gemini_api_key_here
GEMINI_RECOGNITION_MODEL=gemini-2.5-flash
GEMINI_CONTENT_GENERATION_MODEL=gemini-2.5-flash-image

# Google Drive
GOOGLE_DRIVE_MARKETBOT_FOLDER_ID=your_folder_id_here

# Optional
AUTO_GENERATE_CONTENT=True
DEFAULT_USER_TIMEZONE=Europe/Moscow
PUBLICATION_CHECK_INTERVAL=60
USE_PROXY=False
OWNER_TELEGRAM_ID=your_telegram_id_here
```

См. `.env.example` для полного списка переменных.

2. **Настройте Google Sheets API:**
   - Создайте проект в [Google Cloud Console](https://console.cloud.google.com/)
   - Включите Google Sheets API и Google Drive API
   - Создайте Service Account и скачайте credentials JSON
   - Поместите файл в `config/google_credentials.json`

3. **Получите Telegram Bot Tokens:**
   - Откройте [@BotFather](https://t.me/BotFather)
   - Создайте два бота: основной и support
   - Скопируйте токены в `.env`

4. **Получите Gemini API Key:**
   - Перейдите на [Google AI Studio](https://ai.google.dev/)
   - Создайте API ключ
   - Добавьте в `.env`

### Запуск

**Основной бот (AI_SMM):**

```bash
# Рекомендуется для production
sudo systemctl start marketbot.service

# Альтернативные методы
./run_bot.sh                    # Фоновый режим (nohup)
python3 -m src.main             # Прямой запуск (foreground)
```

**Support бот:**

```bash
./run_support_bot.sh           # Фоновый режим
python3 -m src.main_support    # Прямой запуск
```

### Production Deployment

**Управление через systemd (рекомендуется):**

```bash
# Запуск
sudo systemctl start marketbot.service

# Остановка
sudo systemctl stop marketbot.service

# Перезапуск
sudo systemctl restart marketbot.service

# Статус
sudo systemctl status marketbot.service

# Включить автозапуск при загрузке
sudo systemctl enable marketbot.service
```

**Альтернативные методы:**

```bash
# Через скрипт управления
./bot_control.sh start
./bot_control.sh stop
./bot_control.sh restart

# Остановка всех процессов
./stop_bot.sh
./stop_support_bot.sh

# Убить процессы вручную
pkill -f "python.*src.main"
```

**Просмотр логов:**

```bash
# Скрипт просмотра
./view_logs.sh

# Реал-тайм мониторинг
tail -f logs/bot.log          # Основной бот
tail -f logs/support_bot.log  # Support бот
tail -f logs/scheduler.log    # APScheduler

# systemd журнал
journalctl -u marketbot.service -f
```

⚠️ **КРИТИЧЕСКИ ВАЖНО:** Запускайте только **ОДИН экземпляр** каждого бота! Не используйте несколько методов запуска одновременно - это приведет к конфликтам ("terminated by other getUpdates request").

### Структура проекта

```
AI_SMM/
├── src/                      # Исходный код
│   ├── main.py              # Основной бот
│   ├── main_support.py      # Support бот
│   ├── config.py            # Конфигурация
│   ├── google_sheets.py     # Google Sheets интеграция
│   ├── gemini_service.py    # Распознавание товаров
│   └── ...                  # Другие сервисы
├── config/                   # Конфигурационные файлы
│   └── google_credentials.json
├── logs/                     # Логи ботов
├── docs/                     # Документация
│   └── USER_GUIDE.md        # Руководство пользователя
├── enhanced_images/          # Улучшенные AI фотографии
├── .env                      # Переменные окружения
└── requirements.txt          # Python зависимости
```

### Дополнительная документация

**Для пользователей:**
- 📖 [Полное руководство пользователя](docs/USER_GUIDE.md) - детальная инструкция по всем возможностям

**Для разработчиков:**
- 🔧 [CLAUDE.md](CLAUDE.md) - техническая документация для Claude Code
- 📋 [START_BOT_INFO.md](START_BOT_INFO.md) - инструкции по управлению ботом
- 🤖 [SUPPORT_BOT_SETUP.md](docs/SUPPORT_BOT_SETUP.md) - настройка Support бота

---
---

# AI_SMM - Telegram Bots for Wholesale Suppliers

> Automate product catalog and Telegram channel publishing with AI

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/)
[![Telegram Bot](https://img.shields.io/badge/Telegram-Bot-blue.svg)](https://telegram.org/)
[![AI Powered](https://img.shields.io/badge/AI-Gemini%202.5-orange.svg)](https://ai.google.dev/)

**Bots:**
- 🤖 [@iaismm_bot](https://t.me/iaismm_bot) - main bot
- 💬 [@aismm_support_bot](https://t.me/aismm_support_bot) - technical support

---

## 📋 About the Project

**AI_SMM** is a comprehensive solution for wholesale suppliers in marketplaces that helps:
- Manage product catalogs with AI photo recognition
- Automatically publish products to Telegram channels
- Enhance product photos and descriptions using Google Gemini
- Schedule publications automatically
- Generate informative posts (currency rates, news, tips)

### Two Bots in One Project

**[@iaismm_bot](https://t.me/iaismm_bot)** - main working bot
- Product recognition from photos (AI Gemini 2.5 Flash)
- Photo and text enhancement
- Automatic channel publishing
- Price list management
- Informative posts

**[@aismm_support_bot](https://t.me/aismm_support_bot)** - technical support
- Automatic answers from knowledge base
- Support ticket creation
- AI assistant for problem solving
- Integration with main bot

---

## 🚀 Quick Start

### For Suppliers

1. **Open the bot** [@iaismm_bot](https://t.me/iaismm_bot)
2. **Press `/start`** to register
3. **Fill in your profile:**
   - Your name
   - Market name (e.g., "Sadovod")
   - Pavilion number
   - Contact phone
4. **Add Telegram channel** via 📺 CHANGE CHANNEL button
5. **Upload first product** via 📸 ADD NEW PRODUCT button

Done! You get a **free FREE tier** with 5 product publications and 1 informative post per day.

---

## ✨ AI_SMM Features

### 📸 AI Product Recognition
- Send product photo - AI automatically recognizes:
  - Product name
  - Description
  - Material
  - Dimensions/volume
  - Packaging information
- Support up to 10 photos at once
- Edit recognized data

### 🎨 AI Content Enhancement
- **Enhanced photos:** professional backgrounds, quality processing
- **Marketing texts:** selling descriptions for publications
- Choice between original and enhanced content

### 📅 Channel Publishing
**Automatic publishing:**
- Smart post distribution over time
- Morning and evening publication windows
- FIFO product queue

**Manual publishing:**
- Choose exact date and time
- Calendar and time picker
- Publish to multiple channels

### 💰 Price Lists
- Upload PDF, photos, or Google Sheets
- Automatic scheduled publishing
- Manage multiple price lists

### 💬 Informative Posts
Automatic generation:
- 💵 Currency rates (USD, EUR, CNY, TRY)
- ₿ Cryptocurrencies (Bitcoin, Ethereum)
- 📰 Business news (VC.ru)
- 💡 Supplier tips
- 📊 Daily summaries

### 📺 Channel Management
- Add multiple channels
- Custom descriptions for each channel
- Publish to selected channels

### 🔐 Privacy
All contact data (phones, addresses) is added **only locally** and never sent to external APIs.

---

## 💬 Support Bot Features

**[@aismm_support_bot](https://t.me/aismm_support_bot)** - your 24/7 assistant

### Main Functions
- ❓ **Automatic answers** from knowledge base
- 📝 **Create tickets** via `/new`
- 📋 **View tickets** via `/my_tickets`
- 📚 **FAQ** via `/faq`
- 🤖 **AI classification** of issues (bug/feature/question)

### How It Works
1. Ask a question to the bot (just write text)
2. AI searches for answer in knowledge base
3. If not found - ticket is created and operator is notified
4. You can attach screenshots for better understanding

---

## 💎 Pricing Plans

| Plan | Product posts/day | Info posts/day | Features |
|------|------------------:|---------------:|----------|
| **FREE** | 5 | 1 | AI recognition, basic features |
| **START** | 20 | 3 | AI recognition, auto-publishing |

**💡 Important:** Informative posts are **NOT included** in product post limits!
- FREE: 5 products + 1 informative = **6 posts per day**
- START: 20 products + 3 informative = **23 posts per day**

Limits reset daily at **00:01 MSK**.

---

## 📖 How to Use

### Add Product
Press **📸 ADD NEW PRODUCT** → send photo → AI recognizes product → select location → save. Done!

### Publish Post
**📦 MY PRODUCTS** → select product → **📅 Publishing** → choose channel, date and time → confirm.

### Setup Auto-publishing
In product card, enable "Automatic scheduling" option. Bot will publish products automatically every day.

### Upload Price List
**📊 PRICE LIST** → **➕ Add** → choose file (PDF/photo) or Google Sheets link → select channel → set publish time.

### Get Help
Write to [@aismm_support_bot](https://t.me/aismm_support_bot) - AI will answer automatically or create ticket for operator.

**📖 Full documentation:** [User Guide](docs/USER_GUIDE.md)

---

## ❓ Frequently Asked Questions

### How to start using the bot?
Open [@iaismm_bot](https://t.me/iaismm_bot) and press `/start`. Follow the registration instructions.

### Why doesn't the bot publish to my channel?
1. Check that bot is **administrator** in the channel
2. Ensure channel is added via `/channels`
3. Check daily publication limits in your profile

### How do photo enhancements work?
AI (Gemini 2.5 Flash) creates professional product photos: removes background, adds beautiful studio background, improves lighting and quality.

### What are informative posts?
Automatically generated posts with currency rates, crypto, business news and supplier tips. Attract subscriber attention and increase channel activity.

### Are START tier limits enough for me?
START tier (20 products + 3 info posts per day) is suitable for active work. Contact administrator for extended capabilities.

**📚 Full FAQ:** [docs/USER_GUIDE.md](docs/USER_GUIDE.md#часто-задаваемые-вопросы)

---

## 💬 Technical Support

**Have questions or problems?**

- 🤖 Support bot: [@aismm_support_bot](https://t.me/aismm_support_bot)
- 📸 Attach screenshots when describing problems
- 📖 Documentation: [docs/USER_GUIDE.md](docs/USER_GUIDE.md)

**We respond in order of queue!**

---
---

## 🔧 For Administrators

> ⚠️ This section is for developers and system administrators who deploy bots on servers.

### Requirements

- Python 3.9+
- Google Sheets API
- Google Drive API
- Google Gemini API
- Telegram Bot Tokens

### Installation

```bash
# Clone repository
git clone <repository-url>
cd AI_SMM

# Install dependencies
pip install -r requirements.txt
```

### Configuration

1. **Create `.env` file** based on `.env.example`:

```bash
# Telegram Bot Tokens
TELEGRAM_BOT_TOKEN=your_bot_token_here           # Main bot
SUPPORT_BOT_TOKEN=your_support_bot_token_here   # Support bot

# Google Sheets API
GOOGLE_SHEETS_CREDENTIALS_FILE=config/google_credentials.json
GOOGLE_SHEETS_SPREADSHEET_ID=your_spreadsheet_id_here
MARKET_SUPPORT_SPREADSHEET_ID=your_support_spreadsheet_id_here

# Google Gemini API
GEMINI_API_KEY=your_gemini_api_key_here
GEMINI_RECOGNITION_MODEL=gemini-2.5-flash
GEMINI_CONTENT_GENERATION_MODEL=gemini-2.5-flash-image

# Google Drive
GOOGLE_DRIVE_MARKETBOT_FOLDER_ID=your_folder_id_here

# Optional
AUTO_GENERATE_CONTENT=True
DEFAULT_USER_TIMEZONE=Europe/Moscow
PUBLICATION_CHECK_INTERVAL=60
USE_PROXY=False
OWNER_TELEGRAM_ID=your_telegram_id_here
```

See `.env.example` for full list of variables.

2. **Configure Google Sheets API:**
   - Create project in [Google Cloud Console](https://console.cloud.google.com/)
   - Enable Google Sheets API and Google Drive API
   - Create Service Account and download credentials JSON
   - Place file in `config/google_credentials.json`

3. **Get Telegram Bot Tokens:**
   - Open [@BotFather](https://t.me/BotFather)
   - Create two bots: main and support
   - Copy tokens to `.env`

4. **Get Gemini API Key:**
   - Go to [Google AI Studio](https://ai.google.dev/)
   - Create API key
   - Add to `.env`

### Running

**Main bot (AI_SMM):**

```bash
# Recommended for production
sudo systemctl start marketbot.service

# Alternative methods
./run_bot.sh                    # Background mode (nohup)
python3 -m src.main             # Direct run (foreground)
```

**Support bot:**

```bash
./run_support_bot.sh           # Background mode
python3 -m src.main_support    # Direct run
```

### Production Deployment

**Management via systemd (recommended):**

```bash
# Start
sudo systemctl start marketbot.service

# Stop
sudo systemctl stop marketbot.service

# Restart
sudo systemctl restart marketbot.service

# Status
sudo systemctl status marketbot.service

# Enable autostart on boot
sudo systemctl enable marketbot.service
```

**Alternative methods:**

```bash
# Via management script
./bot_control.sh start
./bot_control.sh stop
./bot_control.sh restart

# Stop all processes
./stop_bot.sh
./stop_support_bot.sh

# Kill processes manually
pkill -f "python.*src.main"
```

**View logs:**

```bash
# View script
./view_logs.sh

# Real-time monitoring
tail -f logs/bot.log          # Main bot
tail -f logs/support_bot.log  # Support bot
tail -f logs/scheduler.log    # APScheduler

# systemd journal
journalctl -u marketbot.service -f
```

⚠️ **CRITICALLY IMPORTANT:** Run only **ONE instance** of each bot! Don't use multiple launch methods simultaneously - this will cause conflicts ("terminated by other getUpdates request").

### Project Structure

```
AI_SMM/
├── src/                      # Source code
│   ├── main.py              # Main bot
│   ├── main_support.py      # Support bot
│   ├── config.py            # Configuration
│   ├── google_sheets.py     # Google Sheets integration
│   ├── gemini_service.py    # Product recognition
│   └── ...                  # Other services
├── config/                   # Configuration files
│   └── google_credentials.json
├── logs/                     # Bot logs
├── docs/                     # Documentation
│   └── USER_GUIDE.md        # User guide
├── enhanced_images/          # AI-enhanced photos
├── .env                      # Environment variables
└── requirements.txt          # Python dependencies
```

### Additional Documentation

**For users:**
- 📖 [Complete User Guide](docs/USER_GUIDE.md) - detailed instructions for all features

**For developers:**
- 🔧 [CLAUDE.md](CLAUDE.md) - technical documentation for Claude Code
- 📋 [START_BOT_INFO.md](START_BOT_INFO.md) - bot management instructions
- 🤖 [SUPPORT_BOT_SETUP.md](docs/SUPPORT_BOT_SETUP.md) - Support bot setup

---

**© 2025 AI_SMM. Powered by Google Gemini AI.**
