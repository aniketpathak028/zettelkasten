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
 - uses causal convolution to prevent future samples from being used
 - uses dilated convolution to enable a very large receptive field

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

- conclusions about 3D Voxel CNNs:
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

	- 3D Generative Voxel CNN - Octree Generating Networks
		- given an image of an object predict its shape
		- use an encoder-decoder architecture
		- decoder gradually refines rough estimated low-resolution shape to a higher resolution
		- for every voxel the CNN predicts whether it is occupied, empty, or partially occupied
		- if a voxel is partially occupied, subdivide it further
		![[Pasted image 20260917170439.png]]

Convolutions on Hierarchical 3D CNNs:
- pos
	- Hierarchies can reduce the mem and time complexity
	- Allows 3D CNNs on higher resolution, which leads to better performance
- neg
	- performance at the same resolution can be reduced because feature maps are not at high resolution everywhere
	- still have computation over empty voxels

![[Pasted image 20260917180521.png]]

- hierarchical vol representations subdivide the space adaptively into smaller voxels near the surface. For empty space, larger voxels are used which saves memory
- OctNet CNNs are designed to act as if they were regular convolution on a reg grid at the highest resolution of the hybrid structure, but are implemented such that redundant computations inside nodes are avoided. 
### Sparse CNNs
- Regular 3D Convolution - Dilation Problem
	- convolution operates on both active and non-active sites
- issue - dilation
	- regular convolutions dilates the sparse data in every layer
	- set of active sites (non-zero pixels / voxels) grows rapidly - loss of sparsity!
	- features get diluted - slower propagation
		![[Pasted image 20260918020240.png]]

- Regular Sparse Convolution
	- convolutions that operate only at active sites where the kernel touches an active site
- issue - dilation
	- set of active sites (non-zero pixels / voxels) grows rapidly - loss of sparsity!
	- more efficient than dense conv for sparse data
		- but continual increase in computation and required memory in deeper layers

- Sub-manifold Sparse Convolutions (SSC) or Valid Sparse Convolutions (VSC)
	- restricts convolutions to retain the same set of active sites throughout the network
	- prevents the activation of new sites and preserves the input sparsity pattern
	- kernels are centered only at active locations
		![[Pasted image 20260918020751.png]]

- disconnected components do not communicate in sub-manifold sparse convolutions, how do we resolve this?
	- strided convolutions - stride>1 reduces the spatial resolution and brings sites closer in the lower resolution representation
	- pooling operations - also reduces spatial resolution and creates effective neighbourhood
	- regular sparse convolutions (SC) - controls dilation of the active site
- Sparse Upconvolution
	- inverse of strided regular sparse convolution
	- retains the sparse structure on the same resolution
		- during downsampling, we store the sparse structure
		- during upsampling, we take the prev stored structure
	- used for sparse decoder
	- sparse decoders need to know not just how to upsample features but also where those upsampled feat must stay!

- Minkowski Engine - library for sparse CNNs
	- implements generalized sparse convolution
	- generalizes to 4D and higher dim data
	- covers previous work submanifold sparse conv as a special case
- applications:
	- shape classification
	- 3D semantic segmentation
	- 3D shape generation
	- shape completion
	- 3D Object detection
- conclusions on sparse CNNs:
	- pos
		- features only around the surface
		- requires significantly less mem
		- allows for much higher resolutions and thus better performance
	- neg
		- quantization remains

![[Pasted image 20260918125605.png]]
- reg sparse convolution dilate in each layer resulting in more active sites after each layer. Submanifold sparse convolutions do not change the set of active sites.
- it has 5x5 active sites after first regular sparse convolution and 9x9 after second
	- general formula for a K x K kernel applied N times to a single point the side length Sn of the active bounding square is given by: Sn = 1 + N x (K-1)
	- so for K=5 and N=2 -> S2 = 1 + 2.(5-1) = 1 + 8 = 9 -> 9 * 9 = 81 
### Point Based Networks

- set of 3d points P where each point has additional features - color, reflectivity etc
- issue - irregular variable density
- scanning devices can produce point clouds ex- LIDAR and RGB-D Camera
- Invariances:
    - point permutation invariance - order of the set does not influence predictions
    - spatial transformation invariance - rigid transformation (rotation, translation) should not influence predictions
    - sampling invariance - the process of sampling should not influence predictions but only the underlying geometry!
- PointNet (Vanilla)
    - takes point cloud as input - 2d array
    - can perform - classification, part segmentation or semantic segmentation
    - MLP h transforms points to a high dim feat space
    - max pooling g aggregates all points features usually it is the max pooling fn
    - MLP gamma aggregates pooled features and classifies the point cloud
    - iff g is symmetric then the network is permutation invariant!
    - symmetic fn - for every input permutation the output remain same! ex - sum, add, mean, min, max etc.
![[Pasted image 20260918143541.png]]

- Spatial Transformation Invariance: Spatial Transformer Network
    - make the network spatially invariant using T-Net, it creates a 3 x 3 matix that when multiplied with the input point cloud, we get the transformed point cloud!
    - a regularization loss is added to make the transform matrix T close to orthogonal L_reg = || I - TT^T||^2
    
![[Pasted image 20260918144245.png]]

- PointNet classification and segmentation networks:

![[Pasted image 20260918144454.png]]

![[Pasted image 20260918144504.png]]

![[Pasted image 20260918144706.png]]

![[Pasted image 20260918144847.png]]

![[Pasted image 20260918144855.png]]

- PointNet++
	- applies multiple PointNets at different locations and scales
	- learns hierarchical representation making the network translation invariant
	- in each layer - farthest point sampling -> query ball grouping -> pointnet
![[Pasted image 20260918145526.png]]

- How PointNet++ works in detail!
	
	![[Pasted image 20260918150430.png]]
	
	![[Pasted image 20260918150441.png]]

	![[Pasted image 20260918150951.png]]
	
	![[Pasted image 20260918151134.png]]

	

- Sampling invariances - MSG and MRG in PointNet++
	- PointNet suffers from non-uniform sampling density
	- Use multi-scale and multi-resolution grouping which makes the network more robust to varying sampling densities

![[Pasted image 20260918151215.png]]

![[Pasted image 20260918151447.png]]

- Conclusion on Point-based Networks:
	- pos
	    - fast training + testing → easy to implement (do not need voxelization so avoid quantization problem of grid based methods)
	    - cover large spaces in one shot
	- neg
	    - cannot represent free space unlike grid based methods
	    - performance is worse than volumetric networks!

![[Pasted image 20260918151543.png]]

- It uses max pooling layer to be invariant to point permutation and a Spatial transformer Network T-Net to be invariant to spatial transformations
- concatenate the global feat to each local point features to make the point feat aware of the global information
### Projection based Networks

- Project 3D data into 2D image and apply standard 2D CNNs
- 2 popular choices:
	- Range View - dense, Z-axis preserved, scale variation wrt range and occlusions
	- Birds Eye View - preserves the metric space, sparse at distance
- RangeNet++
	- Network for LiDAR semantic segmentation
	- takes a 2D range image with 5 channels - depth, x, y, z, remission as input
	- segmentation output of the 2D CNN is projected back into the point cloud
	![[Pasted image 20260918152614.png]]

- EfficientLPS - Range-Guided Dilated convolutions
	- adapts the receptive field of convolution by predicting the dilation factor from the range-encoded features
	- captures distant-invariant features
	- employed in the semantic head
	![[Pasted image 20260918152756.png]]

- Conclusions on Projection based networks:
	- pos
		- avoids costly computations in 3D
		- low latency
	- neg
		- spatial info may get lost thro proj
			- ex- clearly separated obj in 3d may look close in 2d
			- perspective proj distorts obj sizes
		- not suitable for all 3d tasks
			- suffers from occlusions
			- not suitable for completion tasks
![[Pasted image 20260918153046.png]]
- it preserves metric space which means that obj sizes are preserved with dist
- EfficientLPS predicts the dilation factor from the range encoded feat to adapt the receptive field, thus handling scale variations

## Links:

202609171153
