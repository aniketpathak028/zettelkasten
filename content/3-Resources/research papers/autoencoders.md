---
title: autoencoders
draft: false
tags:
  - autoencoders
date: 2026-06-17
description: what is an autoencoder?
---
# autoencoder

paper - https://arxiv.org/abs/2201.03898

- taking an image passing it through an autoencoder to get a low dimensional representation in the latent space and then passing it through the decoder to reconstruct the original image from the latent representation!
- ex- if we have a 28x28 image in input, we have 764dim in the input and maybe we can represent it in 64dim in the latent space and then reconstruct it back into the original image using the 64dim latent representation!
- goal: reduce the loss ie MSE (pixel wise loss between the reconstruction and the original image)
- but when we even take a point in the latent space that is near to the original point we get a messy reconstruction because it might represent something meaningful

Limitations:
- random sampling won't work!


![[Pasted image 20260617235900.png]]






## Links:

202606172354
