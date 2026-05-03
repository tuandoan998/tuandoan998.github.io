---
title: "Invoice Parser"
excerpt: "Robust pipeline to ingest messy PDF and image invoices and output structured, validated JSON using OCR and LLM-powered extraction."
header:
  teaser: /assets/portfolio/invoice_parser/mailops_1.png
collection: portfolio
order: 3
tech: ["Document AI", "OCR", "LLM", "Pydantic", "Python"]
---

A document intelligence pipeline that takes raw, unstructured invoices (scanned PDFs, photos, email attachments) and produces clean, validated JSON. The system handles rotation, low resolution, and varied layouts that break generic OCR tools.

## Gallery

![Invoice parser UI 1](/assets/portfolio/invoice_parser/mailops_1.png)

![Invoice parser UI 2](/assets/portfolio/invoice_parser/mailops_2.png)

<video width="100%" controls>
  <source src="/assets/portfolio/invoice_parser/demo.webm" type="video/webm">
  Your browser does not support video playback.
</video>

## Key Features

- **Preprocessing**: Deskewing, denoising, and contrast enhancement before OCR
- **Multi-engine OCR**: PaddleOCR + Tesseract fallback for maximum coverage
- **LLM extraction**: GPT-4 structured output for key-value field extraction from noisy OCR text
- **Validation**: Pydantic schemas enforce type correctness; uncertain fields flagged for human review
- **Supported fields**: Vendor, date, line items, totals, tax, payment terms

## Architecture

```
PDF/Image → Preprocess → OCR → LLM Extraction → Pydantic Validation → JSON Output
                                                        ↓
                                              Human Review Queue (low-confidence)
```
