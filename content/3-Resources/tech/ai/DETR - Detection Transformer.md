---
title: Detection transformer
draft: false
tags:
  - ai
  - detr
  - object-detection
  - transformer
date: 2026-05-30
description: what is DETR and how it works?
---
# DETR - Detection Transformer

- object detection - localization, classification, confidence
- obj detection models - DETR, YOLO, FasterRCNN etc.
- idea: given ip img, the model tries to predict a bounding box
- to determine a rectangle uniquely in an img, we need its - height, width and centroid coordinates (x, y)

#### a naive object detection model
- ground truth = [1, 0, 1, 0.5, 0.5, 0.65, 0.65] which are - prob of dog, prob of cat, confidence, bounding box centroid x, y, height, width
- this naive model has issues like - multiple objects in the same image, multiple number of same classes in the same image etc.
- 






## Links:

202605301813
