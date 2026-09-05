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

- yolo v8n - https://platform.ultralytics.com/ultralytics/yolov8/yolov8n
- license plate dataset - https://universe.roboflow.com/roboflow-universe-projects/license-plate-recognition-rxg4e

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

- Structure of the Dataset
	- train
		- images - images with car number plates
		- labels - txt file
	- valid
		- images
		- labels
	- test
		- images
		- labels
	- data.yaml

![[Pasted image 20260905183407.png]]

- 0 - class id since there is only 1 class number plate







## Links:

202609051640
