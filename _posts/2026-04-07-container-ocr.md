---
title: "Building an OCR System for Shipping Container Numbers"
date: 2026-03-31
permalink: /posts/2026/04/container-ocr/
tags:
  - Machine Learning
  - Computer Vision
  - OCR
  - PaddleOCR
  - Object Detection
  - Logistics
  - Python
excerpt: "A deep dive into building a robust container number recognition system using PaddleOCR, addressing layout variations and leveraging ISO standards for validation."
---

![Container OCR System](/assets/images/container_ocr_banner.png)

Shipping containers are the backbone of global trade. In ports, terminals, and logistics hubs, tracking these containers relies heavily on identifying their unique container numbers. Automating this process using optical character recognition (OCR) can speed up operations and eliminate manual data entry errors.

In this post, I'll walk through the development, architecture, and deployment of a Container Number Recognition System built specifically to tackle the unique challenges of "in-the-wild" container images.

## The Challenge

Container numbers aren't just random strings. They follow the **ISO 6346** standard, consisting of:
- **Owner Code**: 3 uppercase letters (e.g., `BEA`)
- **Equipment Category**: 1 letter (`U`, `J`, or `Z`)
- **Serial Number**: 6 digits (e.g., `123456`)
- **Check Digit**: 1 computed digit (e.g., `5`)
- *(Optional) Size and Type Code*: 4 characters (e.g., `45G1`)

A full string looks like `BEAU1234565 45G1`. 

While standard text recognition might seem straightforward, shipping containers present multiple unique challenges:
1. **Layout variations**: The text can be written horizontally on a single line, split into two horizontal lines, or printed entirely vertically (stacked characters).
2. **Physical conditions**: Containers are exposed to the elements, leading to rust, dirt, peeling paint, and dents.
3. **Environment**: Lighting from harsh shadows, motion blur from moving trucks, and steep camera angles.

To solve this, we cannot just throw an off-the-shelf OCR model at the image. We need an intelligent pipeline.

## System Architecture

Our solution is a multi-stage pipeline powered mainly by the **PaddleOCR** framework. It comprises four steps:

```text
Raw Image
    │
    ▼
[0] Container/ROI Detection (YOLO - Optional)
    │
    ▼
[1] Text Detection (PP-OCRv5_server_det)
    │
    ▼
[2] Text Recognition (SVTR_LCNet + ABINet)
    │
    ▼
[3] Post-Processing (Merging, Regex, & Validation)
```

### 0. Container Detection (Optional)
Before searching for text, we can use an object detection model like YOLO to locate the container itself. This step acts as a Region of Interest (ROI) filter to prevent false positives from other text in the background (like truck license plates or random signs).

### 1. Text Detection
Instead of standard object detection bounding boxes, which struggle with tilted or vertical text, we use **DBNet** (Differentiable Binarization). DBNet predicts a shrunk probability map and generates tight polygons around text lines.

For maximum accuracy, we fine-tuned the `PP-OCRv5_server_det` model. 
> **Data Labeling Tip:** We label the physical lines of text rather than the whole block. For a standard container, we draw separate boxes for the prefix (`BEAU`), the serial (`1234567`), and the size type (`45G1`). This separation makes the model much more robust to layout variations.

### 2. Text Recognition
Once we have our text regions (cropped and perspective-corrected into horizontal patches), we feed them into our recognizer. 

Interestingly, we run **two models in parallel**:
- **SVTR_LCNet**: A fast CNN-Transformer hybrid that excels on regular text.
- **ABINet**: An iterative correction model equipped with a language model, which is better at distinguishing ambiguous characters (like `0` vs `O` or `1` vs `I`).

By fusing their results in the post-processing phase, we recover cases where a single model might fail. We also restrict the model's vocabulary using a custom character dictionary to only alphanumeric characters, significantly improving accuracy.

### 3. Post-Processing & Validation
This is where the magic happens. The post-processing script is the brain that pieces the text fragments back together.

**Text Merging:** We use a two-pass algorithm to merge adjacent text boxes based on distance and alignment gaps. It handles single lines, merges two-line prefixes and serials, and stitches together vertically stacked characters.

**Pattern Matching:** We apply Regex patterns to ensure the merged strings match the `^[A-Z]{4}$` (prefix) and `^[0-9]{7}$` (serial) formats. If a text region gets misread by a single character, we use fuzzy matching libraries as a fallback.

**Check Digit Validation:** Because ISO 6346 numbers include a mathematically computed check digit, we can programmatically verify our OCR results. The check digit is calculated via a weighted sum (modulo 11) of the preceding 10 characters. If the model is unsure between a `B` and an `8`, the check digit calculation instantly flags the incorrect prediction, allowing the system to pick the prediction from our secondary ABINet model instead.

---

## Deployment & Performance

The entire pipeline is wrapped in a **FastAPI** server, exposing endpoints like `/predict` for JSON results and `/predict-vis` for visual bounding box debugging. 

Using a single V100 GPU (with PaddlePaddle), the pipeline is incredibly fast:
- Detection: ~50 ms
- Recognition (2 models, 3 boxes): ~120 ms
- Post-processing: ~2 ms
- **Total Throughput: ~175 ms per image**

For even higher production throughput, the models can be exported to TensorRT (fp16), and the image input resolution can be scaled down.

## Conclusion

Building a robust Container Number Recognition system requires more than just deep learning models; it heavily relies on understanding the domain data. By separating text regions smartly during data labeling, leveraging DBNet for robust polygon detection, fusing multiple recognizers, and enforcing ISO check-digit validation in post-processing, the resulting system achieves high accuracy even on rugged, real-world container images.

The PaddleOCR framework provides an excellent foundation, allowing us to focus on the business logic and deployment architecture.
