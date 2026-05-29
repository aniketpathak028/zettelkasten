---
title: swin transformer
draft: false
tags:
date: 2026-05-26
description: swin transformer
---
# swin transformer

paper link - https://arxiv.org/pdf/2103.14030

- shifted window transformer
- released by microsoft asia team
- proved that transformers could be used to solve any kind of vision problems - classification, segmentation or detection.

### problems with ViT

- attention is costly as it take O(N^2) complexity to calculate attention which means it is directly proportional to the resolution of the image!
  
![[Pasted image 20260526164136.png]]

- the attention complexity increases with the resolution of the image which is a big concern!

### swin transformer architecture

> works on the principle that attention need not be applied on the entire image instead could be calculated on smaller windows of patches!

![[Pasted image 20260526165602.png]]

understanding the dimensions:

- Patch partition: input image -> H x W x 3  -> creating 4 x 4 patches across H and W -> (H/4) x (W/4) x 48 (because there are 3 channels and 16 patches and each patch is 4 x 4 so the number of dimensions to represent each patch is = 4 x 4 x 3 = 48) so the final dim after patch partition is (H/4) x (W/4) x 48
- Linear embedding: in linear embedding we just scale the dimension to C (ie. the dimension which the transformer requires for this architecture) so we multiply our input with a matrix of 48 x C to transform it into our desired dimension ie. (H/4) x (W/4) x C (usually C=96 in swin)
- Patch merging: in patch merging we merge the patches to reduce the number of patches and increase the channel dimension! ideally we merge 2 patches along row and column so a patch of size 4 x 4 becomes 2 x 2 so our dimensions become (H/4) x (W/4) x C -> (H/8) x (W/8) x 4C but we again multiply with 4C X 2C linear projection to change its dim to (H/8) x (W/8) x 2C
- the same thing keeps repeating again and again in further stages as patches get merged and channels get wider, the model gets a better context of rough and smooth edges in the image similar to CNNs

issues:
![[Pasted image 20260529092429.png|554]]


## Links:

202605261605
