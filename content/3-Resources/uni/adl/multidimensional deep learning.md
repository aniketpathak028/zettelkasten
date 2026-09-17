---
title: multidimensional deep learning
draft: false
tags:
  - multidimensional-deep-learning
date: 2026-09-17
description: multidimensional deep learning
---
# multidimensional deep learning

### 3D representations and tasks

- 1d - signals (audio, ecg waves), time series (stock prices, temperature), sequences (gene, text)
- 2d - images (2d grid of pixels) -> networks - 2D CNN, ViT
- 3d - spatial 3D data, video/images seq (vol 3d conv, point cloud - point based neural network and image proj - 3D obj to flatten 2D views)

>the order of the sequence is very imp in 1d, alternating it can lose the meaning of the data! commonly used networks - rnn, 1d-cnn, transformers

rnn:
- time series forecasting, NLP, signal processing
- adv - captures sequential dependencies
- disadv - slower training, less parallelizable

1D cnns:
- signal processing, sensor data analytics
- adv - efficient for local feat extraction
- disadv - not ideal for long-term dependencies

transformers:
- nlp, time-series forecasting, tasks with long-range dependencies
- adv - handling long term dependencies, performing in complex tasks
- disadv - computationally more expensive, data hungry
  
>a 1d convolution is basically a cross-correlation! O(i) = (I * K)(i) = SUM(I(i+m)K(m))

 WaveNet 
 - ip - all prev generated audio samples, predicts - the next sample conditioned on a text
 - uses Causal conv to prevent future samples from being used
 - uses dilated conv to enable a very large receptive field!

- 3D tasks
    - shape classification: classify the shape of the object - chair, aeroplane, laptop etc (use ShapeNet)
    - 3d segmentation: semantic segmentation, instance and panoptic segmentation
    - 3d object detection: 3d volumetric bounding boxes
    - localization: where you are in a given place - place recognition, point cloud registration
    - completion: shape completion, semantic scene completion
    - 3d reconstruction: ip image → 3d shape, 3d occupancy pred

![[Pasted image 20260917132120.png]]
- adv - efficient for local feature extraction, disadv - not ideal for long-term dependencies
- point cloud, vol grids, signed distance fields etc.

### 3D Voxel CNNs

- volumetric grids:
	- reg grid in 3D space stored as 3D array - H x W x D
	- entry in the 3D array is called a voxel
	- each voxel stores some information (feature)
- types of vol grids:
	- explicit
		- occupancy grid - either the voxel is occupied or free (1 or 0)
		- ternary grid - occupied, free or unknown
	- implicit
		- distance fields - voxel stores dist to nearest surface
		- signed distance fields - signed dist to nearest surface
			- pos dist in front of surface (outside obj)
			- neg dist behind surface (inside obj)
- voxelization - convert continuous geometric info into discrete grid
	- convert a point cloud or mesh into a vol grid
	- voxel occupied if there is at least one point within the voxel
	- point feat within voxel can be pooled or extracted with small network - mean or max pool using PointNet!
	- ex- VoxNet (point cloud -> occupancy grid -> convolutions -> classification) uses 3D CNN
		![[Pasted image 20260917144903.png|324]]

- CNN complete - 3D shape completion
	- uses prior for 3D completion of the partial input
	![[Pasted image 20260917145012.png|583]]

- ScanNet - semantic segmentation

![[Pasted image 20260917145141.png|607]]
- computationally expensive because the network runs fwd pass on overlapping chunks repetitively

- ScanComplete
	- fully convolutional - one fwd pass to make the prediction for the whole scene
	- trained on crops
	- works on arbitrary sized scenes due to spatial invariance of CNNs
	- coarse to fine prediction enables high spatial context and high resolution
	![[Pasted image 20260917152956.png]]

- conclusions:
	- pos
		- regular grid is simple - 2D network can easily be extended to 3D
		- can encode free space
		- can encode unknown space
		- can encode distance fields (or other higher-order feat)
	- neg
		- high memory complexity
		- high time complexity
		- need high resolution to capture fine details

![[Pasted image 20260917153925.png]]

- ternary grid - voxel stores if it is occupied, free or unknown
- signed dist field - voxel stores the signed dist to the nearest surface

- the gradient in the dist field points to the surface so the network has direct knowledge of where the surface lies, and due to the sign also whether a point is in front of or behind a surface
### Hierarchical 3D Voxel CNNs

- curse of dimensionality - volumetric grids:
	- % of occupancy gets smaller with increasing resolution
	- inefficient as most voxels are unoccupied in the volume
	- very high memory usage to store the structure with high resolution
- solution - Heirarchical Volumetric Representations or Octree
	- partitions 3D space recursively into cubes called octants and saves memory by dividing the space adaptively, so the non occupied regions can remain coarse while the occupied regions could be of finer resolution
	- however accessing indices in Octree is complicated as compared to volume grids because of its tree structure!
	- 3D Voxel CNN - OctNet
			![[Pasted image 20260917160242.png]]
		- it is observed that most of the activations in dense 3d cnns are near the surface so OctNet introduces:
		    - hybrid grid-octree data structure - restrict max depth of an octree to 3
		    - efficient convolution - avoid unnecessary calc on empty space
		    - pooling + unpooling - pool reduces spat res by 2 along each axis
		- performance
		    - similar to dense at same resolution
		    - can use high res due to less mem usage
		    - high res → high acc
	![[Pasted image 20260917160055.png]]
	
### Sparse CNNs



### Point Based Networks



### Projection based Networks









## Links:

202609171153
