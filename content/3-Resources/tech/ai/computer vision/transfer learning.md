---
title: transfer learning
draft: false
tags:
  - transfer-learning
date: 2026-06-10
description: transfer learning
---
# transfer learning

notes - https://miro.com/app/board/uXjVI9ZVABA=/?share_link_id=268989054435

### results until now:
- linear model with no activation (low acc, high loss)
- 1 hidden layer wiht 128 nodes + ReLU (same acc, lower loss)
- 1 hidden layer with 128 nodes + ReLU + regularization + batch norm + dropout + early stopping (acc increased a bit)

but we never reached 90-95% acc, some better?

### use pretrained models why?
training a deep nn from scratch requires:
- very large dataset
- weeks of computation
- risk of overfitting if dataset is small
when we only have a small dataset it is better to use pretrained embeddings from a model that was trained on a large dataset!

### pretrained embeddings
- extract pre trained features instead of learning them from scratch
- a pretrained model is a nn that has already learned to extract features like:
	- edges
	- textures
	- shapes 
	- object parts
	- full objects
![[Pasted image 20260612114513.png|458]]







## Links:

202606101934
