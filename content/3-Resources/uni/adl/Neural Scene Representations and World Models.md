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
	- we cast rays into the scene from the camera ex - 1 ray per pixel using a pinhole camera model
	- and obtain color info in that direction.
	- For NeRFs the color is determined via simplified volumetric rendering techniques
	- Volumetric Rendering equations:
		- absorption - radiance absorbed in a specific location (through particle)
		- out-scattering - rad scattered in different direction
		- emission - rad emitted at a specific location
		- in-scattering - rad scattered in from other dir and sources
	- Radiance in NeRFs:
		- we simplify and ignore out and in-scattering
		- we do not deal with radiance directly and use just RGB color values
		
		![[Pasted image 20260904150938.png|495]]

		- The idea is to learn c(x,d)- color and sigma(x) - absorption with a neural network
		- instead of calculating the integral we sample distances randomly from bin to not constraint the network to fixed discrete bin locations using traditional alpha-blending
		- Neural Radiance Field - Composition
			- we sample N points along each ray
			- input pos = (x,y,z) and direction d=(theta, phi) into radiance field model to obtain colors and densities
			- compose the final ray colors via the discretized volumetric rendering equation
			- train the network with an L2 loss against the ground truth colors.
		- problems:
			- uniform sampling is inefficient
			- detailed volume/border regions need more samples than empty space
			- therefore we train a coarse and a fine model
			- sample the coarse model uniformly along the ray to obtain volumetric density
			- then use this to create a coarse probability density function for the ray and finally use this probability density to sample with finer model!
			- Hierarchical Volume sampling
			![[Pasted image 20260904153606.png]]

		- NERF architecture
			![[Pasted image 20260904153657.png|416]]
			Density -> depends on position
			Color (RGB) -> depends on pos + viewing dir
	
			- NeRFs depend on sinusoidal pos encoding for inputs without which we might get blurry results. Positional encoding allows NeRFs to capture high freq variations 
			- The color depends on viewing direction without which specular highlights disappear

		-> how we train the network?
			![[Pasted image 20260904155016.png]]

![[Pasted image 20260904155317.png]]

















3. 3D Gaussian Splatting










4. World Models











5. Applications



## Links:

202609041334
