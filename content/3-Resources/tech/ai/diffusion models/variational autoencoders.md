---
title: variational autoencoder
draft: false
tags:
  - vae
  - autoencoders
date: 2026-09-21
description: understanding variational autoencoders
---
# variational autoencoders

- there are some challenges with normal [[autoencoders]]:
	- the latent space is unorganized
	- sampling randomly from the latent space generates no meaningful reconstruction
	- even sampling close to the actual representation does not generate meaningful reconstruction
![[Pasted image 20260922003220.png|360]]

paper - https://arxiv.org/abs/1312.6114

- autoencoder vs VAE
![[Pasted image 20260922104423.png]]

- autoencoder
![[Pasted image 20260922104956.png]]

- VAE
![[Pasted image 20260922105034.png]]

- we are forcing the network to learn a dist with mu and sigma
- 

## Links:

202609212357
