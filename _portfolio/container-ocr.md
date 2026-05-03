---
title: "Container Number Recognition"
excerpt: "Custom OCR pipeline for shipping container number recognition, improving accuracy from 91% to 98.1% through model optimization and post-processing."
header:
  teaser: /assets/portfolio/container_number_recognition/container_1.jpg
collection: portfolio
order: 2
tech: ["PaddleOCR", "OpenCV", "Python", "Post-processing"]
blog_url: "https://tuandoan998.github.io/posts/2026/04/container-ocr/"
---

A production OCR pipeline purpose-built for reading ISO 6346 container numbers from CCTV footage and photos. Standard off-the-shelf OCR achieves ~91% accuracy on this task due to font variations, occlusion, and lighting; this pipeline reaches **98.1%** through custom post-processing and domain-specific model optimization.

## Gallery

![Container image 1](/assets/portfolio/container_number_recognition/container_1.jpg)

![Container image 2](/assets/portfolio/container_number_recognition/container_2.jpg)

![Detection result](/assets/portfolio/container_number_recognition/25d2480b-da1b-44ab-aea5-f29f745ac24e.png)

## Key Features

- **Text detection**: Localizes container number regions under varied lighting and angle
- **Custom post-processing**: ISO 6346 check-digit validation and regex-based correction filters false positives
- **Domain fine-tuning**: PaddleOCR recognition model fine-tuned on logistics-specific character set
- **Production-ready**

## Results

| Metric | Baseline | This Pipeline |
|--------|----------|---------------|
| Accuracy | 91.0% | **98.1%** |
