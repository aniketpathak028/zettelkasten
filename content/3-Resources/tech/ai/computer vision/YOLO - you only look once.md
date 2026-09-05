---
title: YOLO - you only look once
draft: false
tags:
  - yolo
  - object-detection
date: 2026-09-05
description: yolo - you only look once
---
# yolo - you only look once

arxiv - https://arxiv.org/pdf/1506.02640

- real time models - can process 24-30+ fps
- use cases:
	- video surveillance
	- self-driving car
	- face detection
	- crowd monitoring during pandemic

- objective - object detection by annotating bounding boxes!
![[Pasted image 20260905105054.png|408]]

![[Pasted image 20260905105325.png|416]]

- Before YOLO - we literally looked at the image more than once!
	- sliding window detectors (pre CNN) - obj detection using hand made filters (no deep learning)
	- Region proposal + classifier (RCNN)
	![[Pasted image 20260905105633.png]]
	- in R-CNNs the region proposal network propose several sub sections of the image that the model inspects to decide which region has the best overlap with the image, however YOLO needs just a single fwd pass!

- How could we possibly design such a system to detect objects?
	- we could input the image and expect an output in the format like (p_obj, x, y, h, w, p_class1, p_class2) where p_obj= prob that an object is present, x,y= coordinates of the center, h= height, w= width, and p_class1= prob of class 1, and so on!
	- but this method is not scalable because if there are multiple objects or multiple classes we need to scale this vector dimension!

- How YOLO architecture works?
	![[Pasted image 20260905112953.png]]

- in yolo we divide the input image into S x S grid























## Links:

202609050105
