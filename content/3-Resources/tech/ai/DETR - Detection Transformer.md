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
- DETR eliminates anchor boxes and the need for Non Maximum Supression (NMS)
- DETR uses direct set prediction!

#### a naive object detection model
- to determine a rectangle uniquely in an img, we need its - height, width and centroid coordinates (x, y)
- ground truth = [1, 0, 1, 0.5, 0.5, 0.65, 0.65] which are - prob of dog, prob of cat, confidence, bounding box centroid x, y, height, width
- this naive model has issues like - multiple objects in the same image, multiple number of same classes in the same image etc.


### [Anchor boxes](https://www.mathworks.com/help/vision/ug/anchor-boxes-for-object-detection.html)
- predefined bounding box shapes that help an object detection model guess the size and location of objects in an image
- instead of predicting boxes from scratch, the model starts from these fixed "anchor" shapes and adjusts them.
- these anchor box features were hand engineered by humans like - aspect ratios, height, width, etc.
![[Pasted image 20260530185427.png|379]]

### Non maximal supression
![[Pasted image 20260530185649.png]]
![[Pasted image 20260530185822.png|462]]
![[Pasted image 20260530185912.png]]
- NMS is hand crafted
- NMS relied heavily on a fixed IoU threshold, which can remove good boxes or keep bad ones if the threshold is poorly chosen.

### set prediction
- DETR always predicts a fixed number of bounding boxes eg. it predicts 100 bounding boxes, but there is only 1 image in the entire image, it will still have 100 bounding box preds with only 1 pred having the obj inside it!
- why?
	- traditional deep networks cannot natively predict a variable number of outputs
	- a neural net normally produces a fixed size output vector - 1000 classes in ImageNet
	- but in obj detection, we require:
		- a variable number of objects
		- arbitrary positions
		- with arbitrary shapes
		
![[Pasted image 20260530190812.png]]


### architecture

![[Pasted image 20260530234341.png]]
![[Pasted image 20260530234618.png]]
![[Pasted image 20260530234743.png]]
- feature maps are multi channeled with much lower resolution than the original image
![[Pasted image 20260530234915.png]]
- the feature map is flattened before passing to the transformer encoder
- the feature map is of dim - h x w x d where d is the dim needed by the transformer
- usually these tokens are not equivalent to patches because these are low resolution and do not need to be divided into further patches like high res images!

## Links:

202605301813
