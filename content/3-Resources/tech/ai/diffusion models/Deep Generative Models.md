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
- 










## Links:

202609031005
