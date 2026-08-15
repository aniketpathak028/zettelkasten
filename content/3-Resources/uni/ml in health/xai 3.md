---
title: '"Untitled"'
draft: false
tags:
date:
description: '"Untitled"'
---
# xai 3

![[Pasted image 20260815012240.png]]

- for LIME, the neighbouring values are randomly sampled, so it might differ from run to run

![[Pasted image 20260815012517.png]]

- so how do we explain a model with 50000 feat instead of 20?

- KernelSHAP
	- shapley is not scalable so kernelshap scales to many features by fitting a wt linear surrogate
	![[Pasted image 20260815014433.png]]
	- kernelSHAP- regression setup
	![[Pasted image 20260815014647.png]]
- instead of calculating all 2^p coalitions, we only check for a smaller number and then use weighted least squares
![[Pasted image 20260815015236.png]]

![[Pasted image 20260815112655.png]]

![[Pasted image 20260815113120.png]]







## Links:

202608150116
