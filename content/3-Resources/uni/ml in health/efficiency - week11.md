---
title: efficiency
draft: false
tags:
  - ml-for-health
date: 2026-10-24
description: efficiency
---
# efficiency - week11

### challenge 
- a model that is good but needs:
	- data we cannot collect
	- labels we cannot afford
	- or GPU we cannot access in a hospital
	is not a useful tool!

### Efficiency
- performance per unit of resource consumed, a more efficient method reaches the same task performance with less of some resource
- 4 resource limitations in ML for health:
	- Data - rare
	- Expert time - hard to label
	- Computations - GPU not available
	- Hardware - model must run on wearable

![[Pasted image 20261024103936.png]]

- some efficiency methods that save some scarce resources are:
	- Weak supervision - expert time (MIL or CLAM)
	- Foundation models and self-supervision - data and labels
	- Data augmentation - data
	- knowledge distillation - hardware and compute

- 3 kinds of efficiency:
	- data
	- label
	- model

1. data efficiency
	- cost
	- rarity
	- privacy 
	- prospective studies are slow and expensive

	- how to measure data efficiency:
		- performance achieved per unit of training data, we can measure it using the learning curve 
		- sample complexity - the smallest n that reaches a target performance
		- ALC - area under learning curve rewards early gains, high if you learn fast from few samples
	

## Links:

202610241020
