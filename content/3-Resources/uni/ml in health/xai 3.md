---
title: '"Untitled"'
draft: false
tags:
date:
description: '"Untitled"'
---
# xai 3

![[Pasted image 20260815012240.png|534]]

- for LIME, the neighbouring values are randomly sampled, so it might differ from run to run

![[Pasted image 20260815012517.png|549]]

- so how do we explain a model with 50000 feat instead of 20?

1. KernelSHAP
	- shapley is not scalable so kernelshap scales to many features by fitting a wt linear surrogate
	![[Pasted image 20260815014433.png|517]]
	- kernelSHAP- regression setup
	![[Pasted image 20260815014647.png|542]]
- instead of calculating all 2^p coalitions, we only check for a smaller number and then use weighted least squares
![[Pasted image 20260815015236.png|593]]

![[Pasted image 20260815112655.png|572]]

![[Pasted image 20260815113120.png|577]]


2. Deep Learning explanations
	- motivation 
		- heatmaps reveal what experts overlook!
		- new patterns immerge that can explain a scenario better
		- saliency maps - scores each region in the input by how strongly it impacts model pred
		- high acc may be wrong sometimes - clever hans effect or shortcut learning
	- deep nets are differentiable, one backward pass gives saliency value per pixel
		- 3 families of pixel attribution
			- gradient based - compute df/dx at the input, fast (1 bwd pass) ex- vanilla gradient
			- activation based - computes for intermediate feat map activations (coarse but class discriminative) ex- CAM, Grad-CAM
			- removal based - how f' changes when feat are removed (slow) ex- LIME, KernelSHAP
	- Vanilla Gradient
		![[Pasted image 20260815125935.png|541]]
	
		![[Pasted image 20260815125945.png|541]]

	- Integrated gradients
		- fixed flaw of vanilla gradient - gradient saturation or dead ReLUs
		- since deep nn use non linear activation, its local derivative might be 0 because ReLU along that path might be saturated -> leading to blank or incomplete heatmaps
		
		![[Pasted image 20260815133028.png|521]]
		![[Pasted image 20260815135212.png]]
		![[Pasted image 20260815135324.png]]

	- class activation mapping
	










## Links:

202608150116
