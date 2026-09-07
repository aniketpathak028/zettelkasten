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
	- if we did a binary classification ex- {similar=0.2, different=0.8} we would need to run the model for all pairs of samples and the ranking would not be consistent meaning if A is similar to B and B is similar to C that does not mean A is similar to C! 

- how to define and quantify similarity?
	- a positive function that returns a small value when x1 and x2 are similar and a large value when both are dissimilar 
	- we learn inverse similarity rather than similarity itself
	- to determine matching pairs we use a threshold T

![[Pasted image 20260907011312.png]]

solution - constraint the distance D to be a metric - ie. produce a metric space

![[Pasted image 20260907011558.png|656]]


![[Pasted image 20260908001919.png|653]]
- Regression is not well suited because we cannot get direct labels
- Multi-class classification is not scalable and would not handle unseen classes at test time
- Binary-classification would not lead to consistent ranking as well as be inefficient

### Mahalanobis Distance

![[Pasted image 20260908002531.png|660]]

The mahalanobis dist warps, rotates, and scales our data space so that we can measure distances in a way that truly reflects the relationships between our data points.

M is the magic filter which is a square matrix that scales and rotates the space to account for the correlations and variances between different dim. M -> +ve semi definite and symmetric

![[Pasted image 20260908003229.png|662]]

- Siamese Network
![[Pasted image 20260908004408.png|663]]

![[Pasted image 20260908004449.png|500]]

![[Pasted image 20260908005054.png]]

- We must use a metric space or triangle inequality eg. consistent ranking, clustering etc
- Siamese n/w - we process both inputs with the same encoder which have the same shared weights
- We can decompose the matrix M into M=W^T T and then generalize W to any non-linear encoder phi

#### contrastive learning

![[Pasted image 20260908005548.png|623]]

![[Pasted image 20260908005629.png|625]]

![[Pasted image 20260908010759.png|628]]

![[Pasted image 20260908010957.png|632]]

![[Pasted image 20260908011021.png|630]]

Note:
- We can compute gradients and weight updates independently for each encoder
	- we just need to average them afterwards
- contrastive losses are essential for:
	- representation learning
	- self-supervised learning
![[Pasted image 20260908011542.png]]

![[Pasted image 20260908011922.png]]

![[Pasted image 20260908011933.png]]

- Triplet loss is more powerful than the contrastive loss
- it allows for more intra-class variance and doesn't force embeddings to be equal but only requires that there is a margin m between different samples
- We need to sample both +ve and -ve pair so negative mining is essential to make it work!

![[Pasted image 20260908012856.png]]

- pull together similar samples in the embedding space, push away different ones!
- the triplet loss allows for intra-class variance and only requires that there is a margin between +ve and -ve samples. The contrastive loss does not and basically tries to pull similar samples into the exact same location, this can lead to sub-optimal results
- network collapse, sampling















## Links:

202609070039
