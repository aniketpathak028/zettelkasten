---
title: introduction to flow models
draft: false
tags:
  - flow-models
date: 2026-09-25
description: what are flow-models?
---
# introduction to flow models

https://www.pi.website/blog/pi07
https://diffusion.csail.mit.edu/2026/index.html

#### Time dependent vector fields
- A time dependent vector field maps a point 'x' in space and time 't' to a velocity vector
- mathematically we define such field as u(x,t) or just as u<sub>t</sub>(x)
- ex- wind direction (the velocity of wind at every point in space and time would be different)
- interestingly the velocity field is responsible to change the trajectories of points as:

![[Pasted image 20260925120319.png|217]]

![[Pasted image 20260925115841.png]]

- the central question which we want to address is:
	- if a point starts at x<sub>0</sub> at t=0 and follows the vector field, where does the particle reach at a later time?
	- to answer this question we need to solve the above differential equation
	- the idea is to use the velocity vector to advance the point in small time increments
	
#### defining flow

- collection of trajectories which evolve according to the vector field

![[Pasted image 20260925121339.png]]

so in sequence we have Velocity Field -> Trajectories -> Flow



## Links:

202609251146
