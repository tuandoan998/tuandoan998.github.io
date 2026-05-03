---
title: "Person Tracking with PTZ Camera"
excerpt: "Real-time person detection and tracking system that automatically controls a PTZ camera's pan, tilt, and zoom to follow subjects."
collection: portfolio
order: 6
tech: ["YOLOv5", "ByteTrack", "PTZ Control", "Python", "ONVIF"]
---

A real-time surveillance system that detects and tracks people using a combination of YOLOv5 and ByteTrack, then drives a PTZ (Pan-Tilt-Zoom) IP camera to keep the tracked subject centered and appropriately zoomed in the frame.

## Demo

<video width="100%" controls>
  <source src="/assets/portfolio/Person_tracking_PTZcamera/a4uzd41ba21w7n18yhbp.mp4" type="video/mp4">
  Your browser does not support video playback.
</video>

## How It Works

1. **Detect** — YOLOv5 (pretrained COCO) detects persons in each frame
2. **Track** — ByteTrack assigns persistent IDs across frames, handling occlusion and re-entry
3. **Control** — PTZ commands (via ONVIF) are computed from the tracked bounding box:
   - **Pan/Tilt**: offset from box center to frame center → proportional velocity commands
   - **Zoom**: bounding box area ratio → zoom in/out to keep subject at target size

## Key Features

- Smooth tracking with velocity-based PTZ control (avoids jerky motion)
- Handles multiple people: locks onto the primary target (largest or first detected)
- Configurable target area ratio for different use cases (close-up vs. wide)
