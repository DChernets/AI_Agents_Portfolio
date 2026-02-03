# 🚛 Moqup - Transport & Logistics Platform

Comprehensive system for managing deliveries from China, including:
- **AI Chatbot** for client consulting
- **TNVED API** for determining customs codes and calculating customs duties
- **CRM2Sheets** for exporting CRM data to Excel with images
- **Scheduler** for task automation

## 📁 Project Structure

```
Moqup/
├── venv/                     # Shared virtual environment
├── config/                   # Shared configuration files
│   └── google-credentials.json
├── chat_bot/                 # AI chatbot for Telegram
│   ├── ai_chatbot.py        # Main bot file
│   ├── full_prompt.py       # Knowledge base
│   ├── config.py            # Configuration
│   └── .env                 # Bot settings
├── code_tnved/              # FastAPI service for TNVED (port 8000)
│   ├── app/                 # FastAPI application
│   └── .env                 # API settings
├── CRM2Sheets/              # Excel export service (port 8001)
│   ├── app/                 # FastAPI application
│   │   ├── main.py         # Main application file
│   │   ├── config.py       # Configuration
│   │   └── services/
│   │       └── sheets.py   # Excel and image handling
│   ├── field_mapping.py    # Field mapping from CRM
│   ├── .env                # Service settings
│   ├── requirements.txt    # Dependencies
│   └── log_config.json     # Logging configuration
├── scheduler/               # Task scheduler
├── systemd/                 # Systemd configurations
├── requirements.txt         # Shared dependencies
├── start_all.sh            # Start all services
├── start_chatbot.sh        # Start bot
├── start_tnved.sh          # Start TNVED API
├── start_crm2sheets.sh     # Start CRM2Sheets
├── logs.sh                 # View logs
└── README.md               # This file
```

## 🚀 Quick Start

### Managing Services via systemd

All services are configured for automatic startup via systemd:

```bash
# Check status of all services
systemctl status moqup-chatbot
systemctl status moqup-tnved
systemctl status moqup-crm2sheets

# Start a service
systemctl start moqup-crm2sheets

# Stop a service
systemctl stop moqup-crm2sheets

# Restart a service
systemctl restart moqup-crm2sheets

# View logs
journalctl -u moqup-crm2sheets -f
# or
tail -f /opt/moqup/CRM2Sheets/crm2sheets.log
```

### Manual Start (for development)

```bash
cd /opt/moqup

# Start chatbot
./start_chatbot.sh

# Start TNVED API
./start_tnved.sh

# Start CRM2Sheets
./start_crm2sheets.sh

# Start all services
./start_all.sh
```

## 🤖 AI Chatbot (Telegram)

### Features:
- 🎯 Intelligent client classification
- 💬 Consultations based on complete knowledge base
- 📋 Automatic brief collection
- 🔄 Escalation to manager
- 💾 Contextual dialogue memory

### Configuration:
```bash
cd chat_bot
cp .env.example .env
# Edit .env:
# - BOT_TOKEN (token from @BotFather)
# - AI_API_KEY (Gemini API key)
# - MANAGER_CHAT_ID (manager ID)
```

## 🔧 TNVED API (port 8000)

### Features:
- 📦 Determination of TNVED customs codes
- 💰 Calculation of customs duties
- 📋 Information about VAT rates
- ⚡ FastAPI REST API

### Endpoints:
- `GET /api/tnved/search` - Search for TNVED code
- `POST /api/tnved/calculate` - Calculate payments

### Configuration:
```bash
cd code_tnved
cp .env.example .env
# Edit .env:
# - GEMINI_API_KEY
# - POSTBACK_URL
# - PORT=8000
```

## 📊 CRM2Sheets (port 8001)

### Features:
- 📥 Receiving webhooks from CRM
- 📄 Creating Excel files with data
- 🖼️ **Inserting product images into Excel**
- 📦 Automatic order export
- 🔐 Protected webhook endpoint

### Image Settings:

In the `.env` file, you can configure image size:

```bash
# Image size in Excel
# Available values: small, medium, large
IMAGE_SIZE=medium
```

**Size options:**
- `small` - 60x60px (compact, up to 3 images per product)
- `medium` - 100x100px (standard, up to 2 images per product) ← **default**
- `large` - 150x150px (detailed, 1 image per product)

### Configuration:
```bash
cd CRM2Sheets
cp .env.example .env
# Edit .env:
# - GOOGLE_CREDENTIALS_PATH=/opt/moqup/config/google-credentials.json
# - SPREADSHEET_ID (Google Sheets template ID)
# - SHEET_NAME (sheet name, usually Лист1)
# - WEBHOOK_ID (secret ID for protection)
# - IMAGE_SIZE (small/medium/large)
```

### Endpoints:
- `POST /webhook/crm/{webhook_id}` - Receive data from CRM
- `GET /download/{file_id}` - Download generated file
- `GET /health` - Check service health

### How it works:
1. CRM sends POST request with product data
2. Service receives headers from Google Sheets template
3. XLSX file is created via openpyxl
4. Images are downloaded and inserted into the file
5. Download link is returned

### Usage Example:
```bash
# Send data
curl -X POST https://crm.vedpanel.ru/webhook/crm/{WEBHOOK_ID} \
  -H Content-Type: application/json \
  -d '{
    codeOrder: ORDER-001,
    name: Product,
    article: ART-001,
    images: [https://example.com/image1.jpg, https://example.com/image2.jpg],
    ...
  }'

# Response:
{
  status: success,
  download_url: https://crm.vedpanel.ru/download/{file_id},
  products_count: 1,
  order_number: ORDER-001
}
```

## 📦 Dependencies

### Common (requirements.txt):
- `python-telegram-bot==20.7`
- `fastapi==0.115.2`
- `uvicorn[standard]==0.32.0`
- `pydantic==2.9.2`
- `aiohttp==3.9.1`

### CRM2Sheets (CRM2Sheets/requirements.txt):
- `openpyxl==3.1.2` - creating Excel files
- `Pillow==11.1.0` - image processing
- `google-api-python-client` - working with Google Sheets API

## 🔄 Systemd Services

All services are configured for automatic startup at system boot:

- `moqup-chatbot.service` - Telegram bot
- `moqup-tnved.service` - TNVED API
- `moqup-crm2sheets.service` - CRM2Sheets service

Configurations are in `/etc/systemd/system/`

## 📝 Logging

### Service Logs:
- **CRM2Sheets:** `/opt/moqup/CRM2Sheets/crm2sheets.log`
- **TNVED API:** via systemd journal
- **Chatbot:** via systemd journal

### Viewing Logs:
```bash
# Via script
./logs.sh

# Directly
tail -f /opt/moqup/CRM2Sheets/crm2sheets.log
journalctl -u moqup-crm2sheets -f
journalctl -u moqup-tnved -f
journalctl -u moqup-chatbot -f
```

## 🔧 Development

### Updating Code:
```bash
cd /opt/moqup
git pull
source venv/bin/activate
pip install -r requirements.txt

# Restart services
systemctl restart moqup-crm2sheets
systemctl restart moqup-tnved
systemctl restart moqup-chatbot
```

### Adding New Dependencies:
```bash
source venv/bin/activate
pip install package_name
pip freeze > requirements.txt
```

## 🌐 Ports and Endpoints

- **TNVED API:** http://localhost:8000
- **CRM2Sheets:** http://localhost:8001
- **Telegram Bot:** works via polling

## 🔐 Security

- All webhooks are protected with unique IDs
- Credentials for Google API are stored in `/opt/moqup/config/`
- Environment variables in `.env` files
- Temporary files are automatically cleaned up

## 📊 Monitoring

### Checking Service Health:
```bash
# CRM2Sheets
curl http://localhost:8001/health

# TNVED API
curl http://localhost:8000/health

# Systemd status
systemctl status moqup-*
```

## 🛠️ Troubleshooting

### Service won't start:
```bash
# Check logs
journalctl -u moqup-crm2sheets -n 50

# Check configuration
systemctl cat moqup-crm2sheets

# Restart
systemctl restart moqup-crm2sheets
```

### Issues with images:
- Check image URLs availability
- Ensure `openpyxl` and `Pillow` are installed
- Check `IMAGE_SIZE` setting in .env

### Error: address already in use:
```bash
# Check port usage
lsof -i :8001

# Stop process
systemctl stop moqup-crm2sheets
```

## 📞 Service Integration

Chatbot can query TNVED API to get codes and calculations.
CRM sends data to CRM2Sheets via webhooks.

## 📄 Versioning

The project uses Git for versioning. All changes are committed to the repository.

---

**Last Updated:** 2025-12-30
**Version:** 2.0 (added CRM2Sheets with image support)
