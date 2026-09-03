---
title: generative models
draft: false
tags:
  - generative-models
date: 2026-09-02
description: generative models
---
# generative models

- generates o/p but many o/p valid
- if we know p(x) we can sample x ~ p and also estimate the likelihood of o/p
- p(x) does not have to be known explicitly!
- conditional generation - p(x|c)
- diff b/w generative and discriminative models
	- discriminative - p(y|x) -> only 1 true label y for each input x (many-to-one)
	- conditional generative - p(x|c) -> many valid outputs x for a condition c - (one-to-many or many-to-many)
- formulating generative modeling

![[Pasted image 20260902201941.png|468]]
![[Pasted image 20260902202003.png|468]]

- implicit vs explicit representations
	- explicit - directly learn the probability density function using max likelihood estimation method ex- VAEs, Autoregressive GPT etc.
	- implicit - bypass the need to calc exact probability numbers, the dist is learned within the model's weights, instead focuses on generation ex- GANs 

- Types of Generative Models:
	- Autoregressive Models
		![[Pasted image 20260902203357.png|458]]
	- Latent Variable Models
		![[Pasted image 20260902224504.png|469]]
	- Flow-based Models
		![[Pasted image 20260902224605.png|474]]
	- Energy-based Models
		![[Pasted image 20260902224700.png|471]]

![[Pasted image 20260902231033.png]]

- main objectives of generative model is to max -ve log likelihood
- flow-based models - does not need a latent space, takes an intial dist and turns it into output dist.
- latent variable models - sample a latent variable z and then conditionally generates the output based on the prior z.
- directly allows to learn the energy function via NN, the exponential function ensures positivity and partition function ensures normalization.

- Problem with partition function? -> computing it is intractable!
- how to avoid the partition function? gradient of the log p(x) is the score function of p wrt to x
	![[Pasted image 20260902233150.png|493]]
- we can optimize the score (which is independent of the partition function) by minimizing the Fisher divergence which has the same optimum as the max log likelihood

- Denoising Score matching
	![[Pasted image 20260902235007.png]]

	- in order to bypass Z, we take the gradient of the log-likelihood w.r.t input x, this derivative is called score function. The score vector at any specific data point points in the direction where the probability density increases most steeply!








## Links:

202609022007
