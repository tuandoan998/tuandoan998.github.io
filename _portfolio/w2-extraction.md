---
title: "W-2 Tax Extraction Pipeline"
excerpt: "Automated pipeline for ingesting W-2 tax forms, extracting key fields with high accuracy, and routing uncertain cases to human review."
header:
  teaser: /assets/portfolio/w2_tax_extraction/ingress_2010_box13.png
collection: portfolio
order: 10
tech: ["PaddleOCR", "pHash", "ORB/FLANN", "Python", "Human-in-the-loop"]
---

An end-to-end document intelligence pipeline built for W-2 tax forms. The system ingests raw scanned W-2s, classifies the form year/variant, aligns to a reference template, extracts all key fields via OCR, and routes low-confidence cases to a human review queue.

## Gallery

![W-2 2010 box 13 extraction](/assets/portfolio/w2_tax_extraction/ingress_2010_box13.png)

![EIN field detection (2019)](/assets/portfolio/w2_tax_extraction/ingress_2019_ein.png)

![Template definition](/assets/portfolio/w2_tax_extraction/template_define_2010.png)

## Demo

<video width="100%" controls>
  <source src="/assets/portfolio/w2_tax_extraction/demo.webm" type="video/webm">
  Your browser does not support video playback.
</video>

## Architecture

```
Ingest → Preprocess → OCR → Classify → Template Match → Template Extract
                                               ↓
                                     Human Review Queue
                                    (low-confidence fields)
```

### Stage Details

| Stage | Method | Purpose |
|-------|--------|---------|
| Preprocess | Deskew, denoise, binarize | Normalize scan quality |
| OCR | PaddleOCR | Full-page text extraction |
| Classify | pHash perceptual hashing | Identify form year / variant |
| Template Match | ORB + FLANN | Align scan to reference template |
| Extract | Bounding-box crop + OCR | Field-level value extraction |
| Review | Confidence scoring | Route uncertain fields to humans |

## Key Features

- **Year-agnostic**: Handles W-2 variants from multiple tax years via per-year template definitions
- **Robust alignment**: ORB/FLANN feature matching corrects rotation and perspective distortion
- **Human-in-the-loop**: Confidence thresholds route uncertain extractions to reviewers rather than silently failing
- **Optional VLM**: Donut vision-language model as fallback for difficult scans
