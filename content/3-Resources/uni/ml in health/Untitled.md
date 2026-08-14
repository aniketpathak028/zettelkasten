---
title: '"Untitled"'
draft: false
tags:
date:
description: '"Untitled"'
---
# # week-5 : xai 2

1. marginal contribution
	- contribution of an element j to a function f when j is added, holding everything else fixed
![[Pasted image 20260813155108.png]]
![[Pasted image 20260813155653.png]]
![[Pasted image 20260813160648.png]]
- 4 shapley axioms:
	- efficiency - the shapley values sum to the gap between full coalition and empty one
	- symmetry - if v(S U {j}) = v(S U {k}) for S that excludes both then MC_j= MC_k
	- dummy - if v(S U {j}) = v(S) for every S then MC_j= 0
	- additivity - for split in value function, the players shapley values also split MC_J(v+w) = MC_j(v) + MC_j(w)
- Uniqueness theorem - shapley values satisfy all 4 axioms so it is probably fair!
- computational challenge - since there are 2^p coallitions for mc_j exact computation is infeasible!
- shapley values
	- strengths:
		- axiomatic - satisfies axioms
		- model-agnostic - works for any value function
		- interpretable - MC_j has a per player meaning
	- limitations:
		- cost - 2^p coalitions
		- missing-feature semantic - feature absent not possible in ML
		- correlated features - credit can leak to features not used by models


2. SHAP
- we need a data matrix "X" - because in ML we can't skip features, to evaluate coalition S, we plug in stand-in values for feat not is S, drawn from X
- SHAP - Shapley Additive exPlanations
- explains individual predictions of an ML model using Shapley values
	- Shapley - uses shapley values
	- Additive - output = baseline + each feat contribution
	- exPlanation - local explanation 
![[Pasted image 20260813165318.png]]
properties of SHAP:
- post-hoc -> analyzes the model after it has already been trained.
- model-agnostic ->  works with any architecture - xgboost, nn, random forest, svm etc.

SHAP axioms:
- local accuracy - baseline + sum of feat contribution = model pred
- missingness - if feat j is missing from input then mc_j=0
- consistency - changing model such that feat j's marginal contribution increases or decreases but SHAP guaranteed it will never decrease
![[Pasted image 20260814103427.png]]

example:
![[Pasted image 20260814214254.png]]
- step-1 is to calculate the baseline!
![[Pasted image 20260814214639.png]]














## Links:

202608131549
