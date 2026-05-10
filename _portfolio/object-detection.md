---
title: "Object Detection (YOLO)"
excerpt: "Custom-trained YOLO detection models across multiple domains with TFLite conversion for mobile deployment."
header:
  teaser: /assets/portfolio/object_detection/vehicle_mobile.jpg
collection: portfolio
order: 4
tech: ["YOLOv5", "YOLO11", "TFLite", "Python", "Android"]
---

A series of custom object detection models trained on domain-specific datasets using the YOLO family (v5 through v11). Models cover multiple object categories and are exported to TFLite for on-device mobile inference.

## Gallery

![Vehicle detection](/assets/portfolio/object_detection/vehicle.png)

![Cow detection](/assets/portfolio/object_detection/cow.png)

![Vehicle TFLite inference](/assets/portfolio/object_detection/vehicle_mobile.jpg)

![Vehicle TFLite inference with SAHI](/assets/portfolio/object_detection/vehicle_mobile_sahi.jpg)

## Key Features

- **Dataset optimization**: Automated cleaning and augmentation pipeline to remove mislabeled samples
- **TFLite export**: INT8 quantization for real-time inference on Android devices
- **Multi-scale training**: Handles objects across a wide range of sizes
