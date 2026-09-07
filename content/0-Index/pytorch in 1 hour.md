---
title: pytorch in 1 hour
draft: false
tags:
  - pytorch
  - deep-learning
date: 2026-09-07
description: understanding the math behind pytorch
---
# pytorch in 1 hour

![[Pasted image 20260907203154.png]]

![[Pasted image 20260907203355.png]]
![[Pasted image 20260907203526.png]]
![[Pasted image 20260907203709.png]]
![[Pasted image 20260907204013.png]]
.shape -> a tuple describing the dimensions #1 debugging tool
.device -> where the tensor lives. cpu or cuda (GPU)
.dtype -> the data type of the numbers. The default is float32 (because of backprop and gradients)

model weights and biases -> float32 (standard)

#### Autograd - Automatic Differentiation

- it is python's built in gradient calculator, and can be turned on using requires_grad=True
- to tell pytorch a tensor is a learnable param we must set requires_grad=True, doing so pytorch tracks every single operation on that tensor!

![[Pasted image 20260907211204.png]]
	![[Pasted image 20260907211546.png|615]]

![[Pasted image 20260907211634.png]]

#### The difference between * and @ in pytorch

![[Pasted image 20260907212340.png]]

- for @ multiplication m1 col = m2 rows
![[Pasted image 20260907212448.png]]

- when building a linear layer always use @ -> y = X@W + b

#### dim arg

![[Pasted image 20260907212629.png]]
![[Pasted image 20260907212716.png]]
![[Pasted image 20260907212807.png]]
#### selecting data - basic and custom

![[Pasted image 20260907212919.png]]
![[Pasted image 20260907213121.png]]











## Links:

202609072031
