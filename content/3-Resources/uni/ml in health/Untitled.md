---
title: '"Untitled"'
draft: false
tags:
date:
description: '"Untitled"'
---
# # week-5 : xai 2

- marginal contribution
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
	






## Links:

202608131549
