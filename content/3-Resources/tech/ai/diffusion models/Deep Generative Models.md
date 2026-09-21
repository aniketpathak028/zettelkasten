---
title: Deep Generative Models
draft: false
tags:
  - deep-generative-models
date: 2026-09-03
description: Deep Generative Models
---
# deep generative models

- Deep generative model tries to learn the true dist from a set of samples from the true dist
- true dist - ground truth aka P_data(x) (we do not have the true dist as it is vexy complex!)
- predicted dist - the dist learned by the model based on the samples collected from the true dist aka P_phi(x)
- Goal - make the predicted dist as close as possible to the true dist! P_phi(x) ~ P_data(x)
- DGMs take as an input a large collection of real-world examples drawn from an unknown and complex dist and outputs a trained neural network that parametrizes an approx dist
- there are 2 main goals of DGM - realistic generation and controllable generation

![[Pasted image 20260921220325.png|318]]

![[Pasted image 20260921221102.png]]

![[Pasted image 20260921221239.png]]

#### Why are we doing this?

- lets say we have a sample of cat images and we want to train our DGM such that it can learn the underlying dist of cats, if the predicted dist is close the original one, we can sample an arbitrary number of new data points using the sampling methods!

#### How are DGMs trained?

- the params phi are learnt by minimizing the discrepancy between p_data(x) and p_phi(x)
- how do we measure the difference between 2 probability dist? -> KL divergence
![[Pasted image 20260921222603.png]]
- KL divergence compares a true dist P and a model Q
- It is 0 when P = Q and grows as Q becomes worse especially when P(x) is large and Q(x) is very wrong
- KL divergence looks at every possible outcome, checks how much the model's prob differs from reality, weighs it by how often that outcome actually happens, and sums everything up.
- The final number tells how how far the model dist is from the original dist

### Challenges in Modeling Dist

- to model a complex data dist, we can parametrize the prob density func using a nn with params phi, creating a model we denote as P_phi, for P_phi to be valid:

![[Pasted image 20260921231530.png]]

- non-negativity -> can be eliminate by taking exponential fn or square
- enforcing normalization:
	- the crucial part to understand is that the number by which we divide the score to normalize it is also called as a normalizing constant or the partition function
	- for most problems, the partition function is intractable and impossible to calculate, this intractability is a central problem that motivates the development of many different families of deep generative models

- Prominent DGMs:
	1. Energy Based Models
	![[Pasted image 20260921232916.png]]

	- For example imagine that we collect exam scores of 1000 students in a course
	![[Pasted image 20260921233029.png]]

	![[Pasted image 20260921234200.png]]

	- we want to convert this into an energy graph so scores which have a higher density should get a lower energy and scores which have a lower density should get a higher energy. The graph will look as follows:
	
	![[Pasted image 20260921234322.png]]

	- now we convert this into probability which looks as follows:

	![[Pasted image 20260921234416.png]]


2. Autoregressive Models
- predicts the next token based on prev generated tokens

3. Variational Autoencoders
- encoder learns to compresses the input into a small latent space
- the latent space captures hidden structure in the data
- decoder turns the latent code back into a sample like the input

4. Normalizing flows
![[Pasted image 20260921234915.png]]


5. Generative Adversarial Networks
![[Pasted image 20260921235518.png]]

![[Pasted image 20260921235605.png]]




## Links:

202609031005
