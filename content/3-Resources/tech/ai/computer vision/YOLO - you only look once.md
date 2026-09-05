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
- original yolo paper 65k+ citations
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


1. Input and Output

- in yolo we divide the input image into S x S grid where for each grid we need to predict 2 things:
	- bounding boxes + confidence ie. (x, y, width, height, confidence score)
	- output class probabilities (each box would have a highest class probability)

Note:
>  each grid can have multiple (B) bounding boxes and n class probabilities so that we can detect multiple objects i.e. if there are 7x7=49 grids we would have 49 * (2 x 5 + 3) outputs if each grid had 2 bounding boxes and predicted (x, y, width, height, conf) + output class prob for 3 classes

- We also keep our 0 <= x, y <= 1 and 0 <= w, h <= 1 because we want to normalize these values for our NN! how?
	- w -> w/width of image
	- h -> h/height of image
	- x -> (x%s)/s
	- y -> (y%s)/s
![[Pasted image 20260905124257.png|582]]

- how confidence score calc?
![[Pasted image 20260905125446.png]]

confidence = IOU (pred, GT) x P(object)

![[Pasted image 20260905132114.png]]

- since we know each grid can produce multiple bounding boxes we always chose the one with the highest IOU

> What about inference? - We do not have the GT during inference like in training!
> ![[Pasted image 20260905134802.png]]

- Confidence during training = IOU x P(object)
- Confidence during inference = C (confidence predicted directly by the model) x P(class)

Loss Function - Object detection as Regression
- what should we penalize our network for?
	- wrong class prediction
	- bbox location
	- confidence score
![[Pasted image 20260905140739.png]]

- Limitations of YOLO
![[Pasted image 20260905163725.png|488]]







## Links:

202609050105
