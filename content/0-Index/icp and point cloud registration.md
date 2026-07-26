---
title: icp
draft: false
tags:
date:
description: icp and point cloud registration
---
# icp and point cloud registration

- scan registration and alignment are needed because when we use a sensor to generate 3d point clouds we need to align them based on point correspondences to generate the environment
![[Pasted image 20260726141526.png|439]]
![[Pasted image 20260726141627.png|439]]

approach #1 - known point correspondences

![[Pasted image 20260726141751.png|480]]
![[Pasted image 20260726141848.png|479]]
![[Pasted image 20260726141923.png|477]]
![[Pasted image 20260726142041.png|477]]
![[Pasted image 20260726142225.png|476]]
![[Pasted image 20260726142404.png|477]]
![[Pasted image 20260726142432.png|477]]
![[Pasted image 20260726142503.png|478]]

approach #2 - unknown point correspondences

- no direct or optimal solution exists
![[Pasted image 20260726200428.png|445]]
- we can guess the point correspondences and run the same method in step1
![[Pasted image 20260726200540.png|449]]
![[Pasted image 20260726200614.png|449]]

![[Pasted image 20260726200731.png|468]]


## Links:

202607261354
