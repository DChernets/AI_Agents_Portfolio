# Cleaning Tender Processor - AI-автоматизация тендерных документов

**Production-система для автоматической обработки тендеров по клинингу через Google Drive, Gmail, OCR и AI-анализ.**

---

## Обзор

Cleaning Tender Processor отслеживает входящие документы, извлекает данные из файлов, анализирует требования с помощью AI и генерирует расчетные Excel-файлы. Система рассчитана на непрерывную работу в production и защищена от повторной обработки одних и тех же файлов.

---

## Что делает система

- мониторит Google Drive и Gmail на новые документы;
- скачивает DOCX, DOC, PDF, XLS и XLSX;
- извлекает текст из документов и сканов;
- применяет OCR для отсканированных PDF;
- анализирует тендерные требования через Polza.ai;
- генерирует Excel с расчетами;
- учитывает региональные и population coefficients;
- загружает результат обратно в Google Drive;
- ведет учет обработанных файлов и ошибок.

---

## Ключевые возможности

- Service Account + OAuth fallback для Google API;
- retry logic с exponential backoff;
- MD5/checksum validation;
- resumable uploads для больших файлов;
- thread-safe обработка нескольких файлов;
- 6-state lifecycle: pending, downloading, processing, uploading, completed, failed;
- подробные логи и realtime statistics;
- systemd-ready deployment.

---

## Производительность

| Метрика | Значение |
|---------|----------|
| Throughput | 100-500 файлов/час |
| Concurrent processing | 3-10 файлов |
| File size limit | до 50 MB |
| Processing time | 10-60 секунд на файл |
| Daily capacity | 2,400-12,000 файлов |

---

## Технологический стек

| Область | Технологии |
|---------|------------|
| Core | Python 3 |
| Cloud | Google Drive API, Gmail API |
| AI | Polza.ai |
| OCR | Tesseract OCR |
| Documents | PyMuPDF, python-docx, openpyxl |
| Reliability | Tenacity, checksums, retry logic |
| Deployment | Linux VPS, systemd |

---

## Бизнес-эффект

- автоматизация ручного разбора тендерной документации;
- меньше ошибок при переносе данных в расчеты;
- быстрый выпуск Excel-файлов с расчетами;
- непрерывная обработка входящих документов;
- экономия десятков часов ручной работы в неделю.

---

## Статус

| Область | Статус |
|---------|--------|
| Google Drive ingestion | Production |
| Gmail ingestion | Production |
| OCR pipeline | Production |
| AI extraction | Production |
| Excel generation | Production |
| Duplicate protection | Production |
| systemd deployment | Production |

---

*Создано на Python, Google Drive API, Polza.ai, OCR и Excel automation tooling.*
