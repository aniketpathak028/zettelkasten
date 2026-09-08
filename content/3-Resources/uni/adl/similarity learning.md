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

![[Pasted image 20260907011312.png|566]]

solution - constraint the distance D to be a metric - ie. produce a metric space

![[Pasted image 20260907011558.png|564]]


![[Pasted image 20260908001919.png|653]]
- Regression is not well suited because we cannot get direct labels
- Multi-class classification is not scalable and would not handle unseen classes at test time
- Binary-classification would not lead to consistent ranking as well as be inefficient

### Mahalanobis Distance

![[Pasted image 20260908002531.png|568]]

The mahalanobis dist warps, rotates, and scales our data space so that we can measure distances in a way that truly reflects the relationships between our data points.

M is the magic filter which is a square matrix that scales and rotates the space to account for the correlations and variances between different dim. M -> +ve semi definite and symmetric

![[Pasted image 20260908003229.png|577]]

- Siamese Network
![[Pasted image 20260908004408.png|574]]

![[Pasted image 20260908004449.png|500]]

![[Pasted image 20260908005054.png|612]]

- We must use a metric space or triangle inequality eg. consistent ranking, clustering etc
- Siamese n/w - we process both inputs with the same encoder which have the same shared weights
- We can decompose the matrix M into M=W^T T and then generalize W to any non-linear encoder phi

#### contrastive learning

![[Pasted image 20260908005548.png|612]]

![[Pasted image 20260908005629.png|611]]

![[Pasted image 20260908010759.png|613]]

![[Pasted image 20260908010957.png|608]]

![[Pasted image 20260908011021.png|607]]

Note:
- We can compute gradients and weight updates independently for each encoder
	- we just need to average them afterwards
- contrastive losses are essential for:
	- representation learning
	- self-supervised learning
![[Pasted image 20260908011542.png|618]]

![[Pasted image 20260908011922.png|617]]

![[Pasted image 20260908011933.png|616]]

- Triplet loss is more powerful than the contrastive loss
- it allows for more intra-class variance and doesn't force embeddings to be equal but only requires that there is a margin m between different samples
- We need to sample both +ve and -ve pair so negative mining is essential to make it work!

![[Pasted image 20260908012856.png|621]]

- pull together similar samples in the embedding space, push away different ones!
- the triplet loss allows for intra-class variance and only requires that there is a margin between +ve and -ve samples. The contrastive loss does not and basically tries to pull similar samples into the exact same location, this can lead to sub-optimal results
- network collapse, sampling
#### sampling and sample mining

- for triplet loss with a dataset of size N, we have O(N^3) possible triplets -> training with all is computationally infeasible
- we require triplets that fulfill D(xa, xn) < D(xa, xp) + m otherwise Loss_triplet=0 and the model will not learn anything
- negative samples can be classified as:
	- easy negatives - where the loss=0
	- semi-hard negatives - where the -ve points are within the margin
	- hard-negatives - where the -ve points are misclassified
	- common practice - use both hard and semi-hard negatives
- why we cannot use only hard negatives?
![[Pasted image 20260908111819.png|519]]

- The most valuable samples are semi-hard negatives ie 0 < Loss < m

- Offline Mining - generate a list of possible triplets offline and sample from that
	- make a checkpoint of the model
	- use that to compute embeddings for a subset of the dataset
	- generate new triplets using the computed embedding
	- train with these triplets for the next N steps (or epochs)
	- repeat from step1
- Offline Mining - problems
	- we need to compute M= N.3 embeddings in worst case for N triplets
	- need to compare each +ve pair to all other embeddings O(M^3)
	- doing this on whole dataset is infeasible
	- we need to re-compute the embeddings again during training

- Online Mining
- 






## Links:

202609070039
