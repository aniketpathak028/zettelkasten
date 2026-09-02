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
	- conditional generative - p(x|c) -> many valid outputs x for a cond c - (one-to-many or many-to-many)
- formulating generative modeling

![[Pasted image 20260902201941.png|468]]
![[Pasted image 20260902202003.png|468]]

- implicit vs explicit representations
	- explicit - directly learn the probability density function using max likelihood estimation method ex- VAEs, Autoregressive GPT etc.
	- implicit - bypass the need to calc exact probability numbers, the dist is learned within the model's weights, instead focuses on generation ex- GANs 

- Types of Generative Models:
	- Autoregressive Models
		![[Pasted image 20260902203357.png|463]]
	- Latent Variable Models
	- Flow-based Models
	- Energy-based Models




## Links:

202609022007
