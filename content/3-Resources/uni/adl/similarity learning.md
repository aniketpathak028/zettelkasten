---
title: similarity learning
draft: false
tags:
  - similarity-learning
  - adv-deep-learning
date: 2026-09-07
description: similarity learning
---
# similarity learning

- why similarity learning?
	- we can't solve all problems using regression or classification
	- example - face recognition
	- in general tasks like comparison, ranking and recognition need something more!
	- if we used regression to predict a similarity score between 2 faces for example we would need to train our model for all possible pairs of faces which is impossible!
	- if we used classification to recognize a person, we would need to train on every person which is not scalable!
	- if we did a binary classification - {similar=0.2, different=0.8} we would need to run the model for all pairs of samples and the ranking would not be consistent meaning if A is similar to B and B is similar to C that does not mean A is similar to C! 

- how to define and quantify similarity?
	- a positive function that returns a small value when x1 and x2 are similar and a large value when both are dissimilar 
	- we learn inverse similarity rather than similarity itself
	- to determine matching pairs we use a threshold T

![[Pasted image 20260907011312.png]]

solution - constraint the distance D to be a metric - ie. produce a metric space

![[Pasted image 20260907011558.png]]





## Links:

202609070039
