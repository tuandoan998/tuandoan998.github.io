---
title: "Smart Security System"
excerpt: "CCTV-based security system with abandoned object detection, abnormal movement detection, and rule-based intrusion detection."
header:
  teaser: /assets/portfolio/smart_security/img1.jpg
collection: portfolio
order: 8
tech: ["Computer Vision", "OpenCV", "Python", "CCTV", "YOLOv5"]
---

A suite of CCTV analytics modules addressing common security monitoring challenges — reducing false alarms while catching real threats that motion-only detectors miss.

## Gallery

![Abandoned/theft object detection](/assets/portfolio/smart_security/img1.jpg)

![Rule-based detection (pose, object position)](/assets/portfolio/smart_security/img2.jpg)

![Intrusion detection zone](/assets/portfolio/smart_security/img3.jpg)

## Demo

<video width="100%" controls>
  <source src="/assets/portfolio/smart_security/cngnks1plixnmvderqph.mp4" type="video/mp4">
  Your browser does not support video playback.
</video>

## Modules

### 1. Abandoned / Theft Object Detection
Detects objects that appear or disappear in a scene by comparing pixel-level changes against a rolling background model. Triggers alert when an object remains stationary beyond a threshold time, or when a previously stable object vanishes.

### 2. Abnormal Movement Detection
Optical flow-based analysis flags motion patterns that deviate from the expected baseline (e.g., running in a restricted zone, loitering).

### 3. Rule-Based Detection
Configurable rules combining person pose estimation and object position relative to defined zones:
- Person near restricted equipment
- Objects placed outside designated areas
- Crowd density thresholds

### 4. Intrusion Detection
Polygon zone definition with person-trajectory tracking. Alerts fire when a tracked person crosses the boundary into a restricted area.
