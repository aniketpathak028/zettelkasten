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

#### steps:
1. yolo pretrained model
2. fine-tune on license plate data
3. use ocr with some specific constraints

#### Finetuning
	- get annotated datatset of license plates
	- finetune a pretrained YOLO model
	- save the model weights
	- use the saved model

 #### Structure of the Dataset
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

![[Pasted image 20260905183407.png|507]]

- 0 - class id since there is only 1 class number plate
- 7057 training images and 2048 validation images
- model - 130 layers with 3.01M params

![[Pasted image 20260905201342.png|514]]

- What is OCR?
	- OCR can be done through traditional and ML based methods
	- Traditional OCR ex- Tesseract OCR
	- DL based OCR - https://github.com/jaidedai/easyocr
	
	![[Pasted image 20260905202102.png|191]]  ![[Pasted image 20260905202026.png|293]]

### inference

- once we have finetuned our yolov8n model with the license plate dataset, we need to do the following steps:
	- we process the video frame by frame, and for each frame we pass it to our trained YOLOv8n model to attain the bounding boxes of the number plates
	- we do some image processing on these bounding boxes like bicubic resizing, grayscale conversion and otsu-thresholding to better parse our characters using easyOCR.
	- we display the enlarged processed bounding box with a green boundary near the number plate and also display the detected number in white above it
	- since we might misread our numberplate sometimes, we maintain a queue to store the detected number at every frame by dividing the coordinates of the bounding box by 10 since there would be very minimal movement of the car in a few frames, this way we choose the number that appears most frequently in our queue.
	- once we have annotated all the frames in the video we stitch it back as our output video
#### Issues:
- YOLO specific issue - flickering effect due to occlusion, since the position of the car changes in the video, the number plate maybe sometimes visible and sometimes not visible! (need a very well trained YOLO model)
- OCR specific issue - the OCR misreads some numbers or alphabets in the number plates when the image is pixelated, to solve this we use the following techniques:
	- note the number plate readings for 20-30 frames and take the one that has the maximum frequency using a deque.
	- once we get the bounding box of the license plate, increase brightness before passing to OCR.













## Links:

202609051640
