# Tender Manager for a Cleaning Company

**Production document-processing workflow for a cleaning business**

## Business context

The operations team receives tender documents through Gmail and Google Drive. Staff previously had to open mixed office files and scanned PDFs, find the required locations and volumes, apply internal calculations, and assemble an Excel result manually.

## Delivered workflow

The production service:

- monitors the company's Gmail and Google Drive inputs;
- downloads and validates DOCX, DOC, PDF, XLS, and XLSX files;
- extracts text and applies OCR to scanned PDFs;
- uses structured LLM extraction for tender requirements;
- applies the company's lookup and calculation rules;
- generates Excel outputs and uploads them back to Google Drive;
- prevents duplicate processing and records each job state;
- retries recoverable failures and writes production logs for support.

## Engineering decisions

### Mixed document formats

The pipeline selects the appropriate extraction path for office documents, text PDFs, and scans. Results are normalized before AI extraction and business calculations.

### Idempotent processing

File tracking and checksums prevent the same tender from being processed twice. Each job moves through explicit download, processing, upload, completion, or failure states.

### Operational recovery

External calls use retries and backoff. Temporary files are cleaned up, failed jobs remain diagnosable, and the service can recover without reprocessing completed inputs.

## My role

I mapped the existing tender workflow with the business, implemented the Google and document integrations, built the OCR, AI extraction, calculation, and Excel-generation pipeline, and deployed it as a continuously running service.

## Technology

Python, Gmail API, Google Drive API, OCR, LLM extraction, OpenPyXL, PyMuPDF, Tenacity, Linux, and systemd.

## Public case-study boundary

Tender files, credentials, company calculation rules, and production source code are private. This repository documents the delivered workflow and engineering decisions.
