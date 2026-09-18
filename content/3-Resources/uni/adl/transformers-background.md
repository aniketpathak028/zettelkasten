---
title: transformers basics
draft: false
tags:
  - transformer
date: 2026-09-18
description: transformer - recap
---
# Transformers

### neural networks for object detection
- object detection is the most fundamental and extensively researched topics in machine vision
- it requires both identification and localization of objects:
	- identification - classification eg - laptop, table, person etc
	- localization - position and size or bounding boxes
	- other properties - velocity, visibility are also possible

- 2 stage detectors:
	- RCNN
		- extracts region proposal from input image using classical computer vision techniques (no learning or nn)
		- computes features for individual boxes via CNN (only take region of box as input)
		- use linear regressor for box refinement (cropping and resizing) and SVM for classification or object presence
		- slow as the network runs fwd pass for all bounding boxes
				![[Pasted image 20260918211759.png]]

	- Fast R-CNN
		- input image is fed into a CNN to generate a convolutional feature map
		- RoI (region of interest) pooling layer aggregates region proposal to a fixed size
		- unified FCN for regression and classification
		- Fast R-CNN is roughly 9x faster in training and over 200x faster during test
				![[Pasted image 20260918212123.png]]

	- Faster R-CNN
		- learn region proposal with a separate network
		- use anchor boxes of multiple scales and aspect ratios to better handle objects of various sizes
		- reduces detection time to around 0.2 seconds per image, enabling real-time object detection applications
			![[Pasted image 20260918213133.png]]

- 1 stage detector
	- [[YOLO - you only look once]]
		- one CNN for both regression and classification
		- uses a SXS grid, with each cell containing k anchor boxes
		- for each anchor box in each cell:
			- predict final box attributes and confidence score (x, y, h, w, confidence)
			- predict scores for each class (including background)
		- similar to region proposal network but specific for each class
			![[Pasted image 20260918213438.png]]

![[Pasted image 20260918213452.png]]
- extracting region proposals -> computing cnn features
- using a region proposal network

### why transformers?

- sequence modelling
	- sequences are natural representations for text data
	- RNN based models - Seq2Seq, LSTMs, GRUs have traditionally been used to model sequences by capturing contextual relationships
- limitations of RNNs:
	![[Pasted image 20260918214321.png]]
	- limited contextual understanding due to long-term dependency challenges from vanishing gradient problem
	- both vanishing gradient and exploding gradient problem
	- inherent sequential nature leads to slower training
	- high computational load and memory constraints
	![[Pasted image 20260918214430.png]]

![[Pasted image 20260918215103.png]]
- parallelization, efficiency, can capture long term dependencies, no vanishing and exploding gradient problems
- the **fixed-length context vector** that forces the encoder to compress an entire input sequence of arbitrary length into a single vector representation

### the attention mechanism
- The 2 types of attention:
	- self-attention - when the input and the target are the same ex- attention between the words in a sentence
	- cross-attention - focuses on an additional input signal as supplementary info (input and target are different) ex- a text and an image!
	![[Pasted image 20260918220150.png]]

	![[Pasted image 20260918220753.png]]
	- we convert the similarity scores into probabilities and multiply weights w_i x v_i to compute the output as weighted sum of the values
- Scaled Dot Product attention
	![[Pasted image 20260918221007.png]]

![[Pasted image 20260918221151.png]]
- normalizes scores to stabilize training gradients
- converts scores to probabilities ensuring they sum to 1
## Links:

202609181658
