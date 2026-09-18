---
title: transformers for text
draft: false
tags:
  - transformer
  - transformer-for-text
date: 2026-09-18
description: transformers for text
---
# transformer for text

### Transformer Architecture
- blocks of transformers:
	- encoder
	- decoder
	- attention
	- feed-fwd networks (FFN)
	- layer normalization
	- positional encoding

	![[Pasted image 20260918225136.png]]

- input word -> vectors (input embeddings) which contain semantic/linguistic meanings -> fed to the encoder block
- decoder works auto-regressively meaning any prev generated output is fed back into the decoder again!
- Encoder:
	- 6 identical layers (6 encoder blocks as per the original paper)
	- sub layers:
		- a multi-head self-attention layer
		- a token-wise feed forward network
	- integration of residual connections and layer norm in each sub-layer
- Decoder:
	- 6 identical layers
	- adds a third sub-layer for multi-head attention over encoder outputs:
		- incorporates masking to ensure auto-regressiveness, allowing predictions for position i depends solely on prior outputs
		- utilizes a triangular masking matrix to prevent future information from affecting current predictions

- Attention mechanism
	![[Pasted image 20260918230220.png]]

- Full masking for bidirectional modelling - attends to the words before, after and itself (used in the encoder)
- Triangular masking for unidirectional modelling - only attends to preceding words and itself (used for generating text in the decoder) by masking with large -ve numbers whose softmax is 0

- Multi-head Attention Mechanism
	- enhances the ability to capture more complex relationships by focusing on multiple aspects of the input
	- combines multiple scaled dot product attention modules as attention heads
	- each head independently focuses on different parts of the input - semantic, linguistic, etc
	- finally we concatenate the output of all the heads and pass the output through the linear layer 
								![[Pasted image 20260918234243.png]]

> one limitation of attention is that it is permutation invariant

- positional encoding
	- to overcome this limitation of attention we use positional encoding which helps the model understand the sequence of the tokens
	![[Pasted image 20260918234607.png]]

- Layer Normalization

> Note: we do not use batch norm because our sequences can be of varying length and that might make it unstable or inaccurate instead layer norm works for each token independently

![[Pasted image 20260918235016.png]]

- Feed Forward Networks
![[Pasted image 20260918235838.png]]

- Why self-attention in transformers? 
![[Pasted image 20260919000437.png]]

- Parallelization - self-attention enables greater parallelization by involving a constant number of sequentially executed operations
- Path-length for long-range dependencies - minimizes the path length that signals need to traverse in the network
- 










### Classifications of Transformers



### Advanced Transformer Variants








## Links:

202609182212
