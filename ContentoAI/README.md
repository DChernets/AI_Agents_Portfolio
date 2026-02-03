# ContentAI - Telegram Channel Automation

SaaS platform for automated Telegram channel management with AI.

## 🚀 Features

- **Automated onboarding** through Telegram bot
- **Smart content collection** from RSS and Telegram channels
- **AI-powered unique post generation** with style preservation
- **Post scheduler** with optimal timing
- **Post performance analytics**

## 📋 Requirements

- Python 3.11+
- PostgreSQL 15+
- Redis 7+
- Docker & Docker Compose (recommended)

## 🛠️ Installation & Setup

### Method 1: Docker Compose (Recommended)

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd contentai
   ```

2. **Configure environment variables**
   ```bash
   cp .env.example .env
   # Edit .env with your API keys
   ```

3. **Start the project**
   ```bash
   docker-compose up --build
   ```

4. **Initialize the database**
   ```bash
   docker-compose exec app python scripts/init_db.py
   ```

### Method 2: Local Development

1. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

2. **Set up PostgreSQL and Redis**
   ```bash
   # Ensure PostgreSQL and Redis are running
   # Create contentai_db database
   ```

3. **Configure environment variables**
   ```bash
   cp .env.example .env
   # Edit .env file
   ```

4. **Initialize the database**
   ```bash
   python scripts/init_db.py
   ```

5. **Run the application**
   ```bash
   python app/main.py
   ```

## 📁 Project Structure

```
contentai/
├── app/                    # Main application
│   ├── api/               # API routes
│   ├── models/            # Database models
│   ├── services/          # Business logic
│   └── utils/             # Utilities
├── config/                # Configuration
├── scripts/               # Scripts
├── tests/                 # Tests
├── logs/                  # Logs
└── docker-compose.yml     # Docker configuration
```

## 🔧 Configuration

Main environment variables in `.env`:

- `TELEGRAM_BOT_TOKEN` - Telegram bot token
- `GEMINI_API_KEY` - Gemini API key
- `DATABASE_URL` - PostgreSQL connection URL
- `REDIS_URL` - Redis connection URL

## 🤖 Usage

1. **Create Telegram bot** via @BotFather
2. **Get API key** Gemini AI
3. **Start the bot** with `/start` command
4. **Complete onboarding** - specify topic, audience, sources
5. **Start automated content publishing**

## 📚 API Documentation

After startup, API documentation is available at:
- Swagger UI: `http://localhost:8000/docs`
- ReDoc: `http://localhost:8000/redoc`

## 🧪 Testing

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=app

# Run specific test
pytest tests/test_telegram_bot.py
```

## 📊 Monitoring

- **Logs**: `logs/app.log`
- **Health check**: `http://localhost:8000/health`
- **Metrics**: `http://localhost:8000/metrics` (coming soon)

## 🤝 Development

### Adding New Features

1. Create model in `app/models/`
2. Add business logic in `app/services/`
3. Create API endpoint in `app/api/`
4. Add tests in `tests/`

### Service Structure

- `TelegramBotService` - Telegram API integration
- `ContentSourcingService` - content collection from sources
- `AIGenerationService` - AI-powered content generation
- `PublishingService` - post publishing
- `SchedulerService` - task scheduling

## 📝 License

Copyright © 2025 ContentAI. All rights reserved.

This software product is protected by copyright law. Any copying, distribution, or use without written permission from the copyright holder is prohibited.

For commercial licensing inquiries, please contact us:
- Telegram: @ContentAI_Support
- Email: support@contentai.ai

## 🆘 Support

If you have questions or issues:
1. Check [FAQ](docs/FAQ.md)
2. Search existing [Issues](../../issues)
3. Create new Issue with problem description