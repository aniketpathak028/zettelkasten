---
title: clustering
draft: false
tags:
  - ml-for-health
  - clustering
date: 2026-08-15
description: patient stratification and disease subtypes
---
# clustering

![[Pasted image 20260815180455.png]]

- Simpson's paradox
	- a trend that appears in every subgroup of the data reverses (or disappears) when subgroups are pooled due to confounder - a 3rd var that drives both subgroup + outcome
	- model trained on aggregate cohort can pick up the wrong sign of an effect if the confounder is unobserved!

- Patient stratification
	- dividing patients into subgroups that will receive same clinical actions - treatment, prognosis, placement
		- risk stratification 
		- treatment stratification
		- trial enrichment
	- grouping variable is already known (supervised)

- disease subtypes
	- distinct biological or clinical entitites hiding inside what was thought to be one disease revealed by patterns in measurements!
		- molecular
		- clinical phenotypes
		- pathophysiological
	- discovered from data, no subgroup label exists beforehand (unsupervised)

- finding subgroups
	- dim reduction - pca, t-sne, umap, vae
	- clustering - k-means, gmm

## Links:

202608151734
