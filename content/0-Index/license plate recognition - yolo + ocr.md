---
title: License plate recognition using YOLO + OCR
draft: false
tags:
  - yolo
  - ocr
  - license-plate-recognition
  - cv
date: 2026-09-05
description: building a license plate recognition using YOLO and OCR
---
# License plate recognition using YOLO and OCR

yolo v8n - https://platform.ultralytics.com/ultralytics/yolov8/yolov8n
license plate datatset - https://public.roboflow.com/object-detection/license-plates-us-eu

we would be using yolo v8n from ultralytics for this problem statement and since it is trained on COCO dataset, it does not contain license data as part of its training so we need to finetune it with a license plate dataset

steps:
1. yolo pretrained model
2. fine-tune on license plate data
3. use ocr with some specific constraints

- Finetuning
	- get annotated datatset of license plates
	- finetune a pretrained YOLO model
	- save the model weights
	- use the saved model









## Links:

202609051640
