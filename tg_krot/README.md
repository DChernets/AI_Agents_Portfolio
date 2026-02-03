# TG Krot - Telegram Lead Generation Bot

System for automatic lead generation from Telegram chats using Gemini AI for filtering.

## Architecture

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

## Installation

### 1. Clone and dependencies

```bash
cd /Users/rocksteady/myAI/TG_Krot
pip install -r requirements.txt
```

### 2. Environment variables configuration

Copy `.env.example` to `.env` and fill in:

```bash
cp .env.example .env
```

Required variables:
- `TG_API_ID` - get from https://my.telegram.org
- `TG_API_HASH` - get from https://my.telegram.org
- `TG_PHONE` - phone number for userbot (account with "aging")
- `BOT_TOKEN` - token from @BotFather
- `MANAGER_CHANNEL_ID` - channel ID for leads (e.g., -1001234567890)
- `ADMIN_IDS` - admin IDs separated by commas
- `GEMINI_API_KEY` - key from https://makersuite.google.com/app/apikey

### 3. Database initialization

```bash
python scripts/init_db.py
```

## Usage

### Running

```bash
python src/main.py
```

### Bot Commands

- `/start` - Main menu
- `/stats` - Statistics
- `/keywords` - Keywords management
- `/groups` - Groups management

## Project Structure

```
TG_Krot/
├── .env                          # Configuration
├── requirements.txt              # Dependencies
├── config/
│   └── settings.py               # Settings (Pydantic)
├── src/
│   ├── main.py                   # Entry point
│   ├── storage/
│   │   ├── database.py           # Database
│   │   └── models.py             # SQLAlchemy models
│   ├── collector/
│   │   └── userbot.py            # Pyrogram userbot
│   ├── filter/
│   │   ├── ai_filter.py          # Gemini AI filter
│   │   └── rules.py              # Basic rules
│   ├── delivery/
│   │   └── bot.py                # Telegram bot
│   └── management/
│       ├── menu_handlers.py      # Inline menu
│       └── telegram_helpers.py   # Helpers
└── scripts/
    └── init_db.py                # Database initialization
```

## Adding Groups for Monitoring

### Method 1: Via bot

1. Send `/groups`
2. Press "➕ Add group"
3. Send group link or username
4. Join the group with the userbot account
5. Get chat_id via @getidsbot
6. Update in database

### Method 2: Directly in DB

```sql
INSERT INTO monitored_groups (chat_id, title, username, invite_link, is_active)
VALUES (-1001234567890, 'Group Name', 'username', 'https://t.me/joinchat/...', true);
```

## Adding Keywords

Via bot:
1. Send `/keywords`
2. Press "➕ Add keyword"
3. Enter word or phrase

## Lead Format in Channel

```
🔥 **NEW LEAD** [8.5/10]

👤 **From:** Ivan Ivanov (@username)
📍 **Chat:** Chinese Goods
🔗 **Link:** [message link]

💬 **Text:**
Looking for electronics supplier...

📊 **AI Analysis:**
- Urgency: 🔴 High
- Budget: $5000-10000

📞 **Contacts:**
- Phone: +7...

[✅ Contact] [📁 Archive] [🚫 Spam]
```

## Gemini API Cost

- gemini-2.5-flash: ~$0.30 per 1M tokens (input)
- Approximate analysis of 1 lead: ~500 tokens
- Cost of 1 lead: ~$0.00015 (0.15₽)

## Scaling

For 50+ chats:
- SQLite → PostgreSQL
- Add Redis for queues
- Multiple workers

## Troubleshooting

```bash
# Check logs
tail -f logs/tg_krot.log

# Test Gemini API
python -c "from src.filter.ai_filter import initialize_gemini_filter; import asyncio; asyncio.run(initialize_gemini_filter())"
```

## License

MIT
