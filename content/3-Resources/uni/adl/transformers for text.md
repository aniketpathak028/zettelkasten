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

- Illustrative example of transformers:
	- first the inputs are converted into embeddings and positional encoding is added 
	- each word is a token with a specific learn representation or embedding
	- multi-head attention captures the attention between different tokens in the sequence
	- add+norm + feed fwd - full understanding of the sentence identifying imp words and relationships
	- decoder output embeddings - begin constructing while looking at previous translations
	- decoder masked-multi-head attention - determine the best words for translation on what has been translated so, without looking ahead(masked)
	- decoder MHA - utilize the prev translation and the newly input text to identify the most likely words
	- feed-fwd + add norm - normalize the data and transform it
	- linear + softmax - generate output words
![[Pasted image 20260919003732.png]]

![[Pasted image 20260919003812.png]]
- transformers inherently do not account for the order of tokens, as the attention mechanism is permutation-invariant. To encode word order, positional encodings is required.
- To make sure word only attends to preceding words and itself Triangular masking is used aka Causal masking
### Classifications of Transformers

- classification by architecture:
	- Encoder only transformer - specializes in processing input data eg. BERT
	- Decoder only transformer - focused on generating outputs from learned representations eg. GPT
	- Encoder-Decoder transformer - combines both functionalities, ideal for tasks like translation (eg. the original transformer model, T5)
- BERT (Bidirectional Encoder Representations from Transformers)
	- BERT is designed primarily for transfer learning
	- Pre-trained with 2 self-supervised objectives, then fine-tuned on downstream tasks
	- No human-annotated data needed, allows for training on vast, unlabelled datasets
	- 







### Advanced Transformer Variants








## Links:

202609182212
