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
	- discriminative - p(y|x) -> only 1 true label y for each input x (many-to-one) ex- classification
	- conditional generative - p(x|c) -> many valid outputs x for a condition c - (one-to-many or many-to-many)
- formulating generative modeling

![[Pasted image 20260902201941.png|468]]
![[Pasted image 20260902202003.png|468]]
Maximizing likelihood = Minimizing -ve log likelihood

- implicit vs explicit representations
	- explicit - directly learn the probability density function using max likelihood estimation method ex- VAEs, Autoregressive GPT etc.
	- implicit - bypass the need to calc exact probability numbers, the dist is learned within the model's weights, instead focus on generation ex- GANs 

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

- main objectives of generative model is to minimize -ve log likelihood
- flow-based models - does not need a latent space, takes an intial dist -> o/p dist.
- latent variable models - sample a latent variable z and then conditionally generates the output based on the prior z.
- directly allows to learn the energy function via NN, the exponential function ensures positivity and partition function ensures normalization.

- Problem with partition function? -> computing it is intractable!
- how to avoid the partition function? gradient of the log p(x) is the score function of p wrt to x
	![[Pasted image 20260902233150.png|493]]
- we can optimize the score (which is independent of the partition function) by minimizing the Fisher divergence which has the same optimum as the max log likelihood

- Denoising Score matching
	![[Pasted image 20260902235007.png]]

	- in order to bypass Z, we take the gradient of the log-likelihood w.r.t input x, this derivative is called score function. The score vector at any specific data point points in the direction where the probability density increases most steeply!
	
	![[Pasted image 20260903120610.png|531]]
	![[Pasted image 20260903120730.png|532]]
	![[Pasted image 20260903124010.png|533]]
	![[Pasted image 20260903124518.png|534]]
	![[Pasted image 20260903124610.png|532]]
	- we must add a small noise to avoid the convergence case!

- Noise Conditional Score Networks (NCSN)
	- for regions with low-density, the noise based score estimate is inaccurate so we artificially enlarge the dist by adding stronger noise
	- large noise corrupts data, so we use multiple noise levels, in training we sum up the losses over noise levels 
	![[Pasted image 20260903131542.png]]

	![[Pasted image 20260903131604.png]]

- benefit -> we do not need to deal with the partition function as the score does not depend on normalization constant and since the score is real values function without any constraints, it can be directly approximated by a neural network
- score (moves the sample towards more probable region of the target dist) and the noise level (required to actually model the dist)
- because for lower noise, the density is lower at many regions causing inaccurate score estimates, but since larger noise reduce acc, use both large and small noise!

- Diffusion models
	- Denoising Diffusion probabilistic Models
		- we first try to learn how to create noise from data q(z|x)
		- then we try to reverse learn how to obtain data p(x|z) from q(z|x)
		- similar to variational auto-encoders but trying to learn in a single step is difficult hence we break it into smaller, iterative steps that are easier to learn
		- q(z|x) is called forward diffusion process which yields a markov chain
			![[Pasted image 20260903153315.png|520]]
		- from noise to data - backward diffusion process leads to a similar Markov chain
			![[Pasted image 20260903153618.png|525]]
		- Training a DDPM -> predicting the noise contained in a noisy sample!
		- DDPM is score matching!
			- training with denoising objective
			- the update step is however different from the denoising score matching problem
		![[Pasted image 20260903161327.png]]
		![[Pasted image 20260903164628.png]]
		- because it is easier for the network to learn small denoising steps. From pure noise, it is hard to infer a realistic sample in one shot, taking small steps is much easier!
		- both add noise to the original sample and try to denoise it, in DDPM the model predicts the noise that was added to x, this predicted noise is directly related to the score of the noisy distribution, which connects DDPMs to denoising score matching and score-based models
		- approximated with a lower bound, it tells us that we can optimize it by training a noise estimator
	- Continuous-time Diffusion
		- infinitely many steps, taking dt=0 leads to SDE - Stochastic Differential Equation
			![[Pasted image 20260903175504.png|407]]
		- Reverse process - we start with random noise at t=1 and solve the SDE backwards in time to t=0
			![[Pasted image 20260903180332.png|427]]
		- Our SDE has a corresponding ordinary differential equation (ODE) inducing the same Pt(x) called probability flow ODE which is deterministic and no stochastic process is needed.
		- Discretizing the ODE leads to Denoising Diffusion Implicit Models
		- Benefits of ODE:
			- no random noise is injected during generation which allows for completely deterministic sampling paths!
			- discretizing the ODE yields Denoising Diffusion Implicit Models (DDIM)
			- bridges diffusion models to CNF and flow matching

	- Diffusion - conclusion
		- diffusion is basically training a denoiser or noise eliminator
		- usually implemented as a single network with time as input (S(x,t)) where t is encoded using sinosudal embeddings (or similar)
		- sampling and training are disjoint (so we need to scale and reparametrize accordingly)

	![[Pasted image 20260903185017.png]]
	- SDE formulation allows us to choose f and g flexibly
	- we can use any ODE solver and since it is deterministic, it allows interpolation in the latent space!



## Links:

202609022007
