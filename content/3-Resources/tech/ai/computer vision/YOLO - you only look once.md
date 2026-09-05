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
	- 
## Links:

202609050105
