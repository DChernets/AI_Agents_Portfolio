# Industrial Automation - Contract and Engineering Document Review

**AI-assisted automation system for industrial engineering document workflows.**

---

## Overview

Industrial Automation helps engineering companies reduce manual document review work across contracts, technical documentation, and project deliverables. The system combines deterministic rules, document parsing, OCR, and LLM analysis with human approval checkpoints.

The solution is designed for industrial projects where accuracy, traceability, and confidentiality matter more than fully autonomous decisions.

---

## Modules

### Contract Review
Automated review of customer contracts against internal templates and risk rules:
- Compares customer contract drafts with the company's preferred contract language
- Detects legal, commercial, delivery, warranty, IP, and liability risks
- Generates a protocol of disagreements
- Proposes alternative wording and commercial rationale
- Marks which items require legal, financial, commercial, or executive approval

### Project Documentation Validation
Cross-document consistency checks for engineering deliverables:
- Validates PDF, DOCX, XLSX, and DWG-derived data
- Cross-checks EM, ATX, TX/P&ID sections
- Detects mismatches in KKS codes, cables, signals, equipment, specifications, and revisions
- Produces a structured issue table with document/page/sheet references
- Prioritizes findings by severity and recommends engineer actions

---

## Key Features

- Contract risk extraction
- Protocol of disagreements generation
- Source data completeness checks
- Project document registry
- OCR and table extraction from technical documents
- Cross-document validation rules
- CAD/PDF processing pipeline for drawing-derived text
- Human approval workflow for legal and engineering decisions
- Confidentiality-first processing model

---

## Typical Workflow

```text
Input documents
      |
      v
Parsing / OCR / table extraction
      |
      v
Structured project data and document registry
      |
      +--> Contract Review -> Protocol of disagreements
      |
      +--> Documentation Validation -> Issue table and engineer recommendations
      |
      v
Human approval and final export
```

---

## Tech Stack

| Area | Technologies |
|------|--------------|
| Backend | Python 3.10+, async processing |
| Documents | PDF, DOCX, XLSX parsing |
| OCR | OCR pipeline for scans and drawings |
| AI | LLM-assisted analysis and explanation |
| Rules | Deterministic validation rules |
| Output | Word and Excel generation |
| Engineering data | KKS, cable journals, specifications, revision tables |

---

## Business Impact

- Faster preparation of contract disagreement protocols
- Earlier detection of missing source data
- Reduced manual cross-checking across engineering documents
- Better traceability of risks and inconsistencies
- Clear approval flow for sensitive legal and technical decisions

---

## Status

| Module | Status |
|--------|--------|
| Contract Review | Implemented |
| Protocol of Disagreements | Implemented |
| Source Data Checks | Implemented |
| Project Document Registry | Implemented |
| Cross-Document Validation | Implemented |
| CAD/DWG Pipeline | Implemented as staged processing |

---

*Built for industrial engineering teams working with contracts, technical specifications, drawings, and project documentation.*
