---
title: Neural Scene Representations and World Models
draft: false
tags:
  - nerf
  - world-models
date: 2026-09-04
description: neural scene representations and world models
---
# NERF

1. Novel view synthesis

	- problem - given a set of images with calibrated camera poses.
	- train a scene representation aloowing us to easily
	- predict a new image of the scene using an unseen target camera pose.

	- application - entertainment - AR/VR, real world perception, simulating novel scenarios - autonomous driving

	- how to obtain calibrated camera poses?
		- use structure from motion methods ex-COLMAP

	![[Pasted image 20260904142943.png|486]]
	- a calibrated camera pose contains everything needed to project 3D points into the image which includes the camera's position, orientation, and typically its intrinsic parameters such as focal length.
	- it tells where the image was taken from, by allowing us to relate observations across different views and reason about the 3D structure of the scene
	- hardly, as a single image only provides  a part of the scene and limited geometric info!

2. Neural Radiance Fields (NeRFs)








3. 3D Gaussian Splatting










4. World Models











5. Applications



## Links:

202609041334
