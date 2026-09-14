---
title: graph neural networks
draft: false
tags:
  - graph-neural-network
date: 2026-09-15
description: graph neural networks
---
# Graph neural networks

### why graphs?

- graphs are straight forward representation of unstructured, distributed and sparse entities that are related or involve interaction.
- graphs are a superset of text, images and also arbitrary related distribution
- complex domains have rich relational structure, which can be represented as a relational graph

![[Pasted image 20260915002411.png]]

1. CNNs and LSTMs are good for structured data with regular structure, however for unstructured data these models fail to work well. 
	- CNNs rely on spatial invariance and local correlation which means they assume features are close together are related and the feat learned in one part of the data looks the same in another part.
	- LSTMs require data to follow an ordered sequence where the current outcome depends heavily on past states.
2. text could be seen as chain of tokens and images as a graph of pixels

### graph structures

- n - nodes (or vertices), e -  edges (can be directed or undirected)
- Node attributes -> X = N x D where N=no of nodes, D=dim of each node data
- Edge attributes -> E = E x C where E=no of edges, C=no of channels/dim for each edge
- connectivity in graph can be defined by an adj matrix
- undirected graph → adj matrix is symmetric
- directed graph → adj matrix is not symmetric

![[Pasted image 20260915003932.png]]

3 general types of prediction tasks:

- node level pred - predicts the node attribute of a GNN
- edge level pred - predicts the edge attribute of a GNN
- graph level pred - predicts the overall graph attribute or properties

![[Pasted image 20260915004358.png]]

X - Node Features, A - Adj Matrix, H - embedding matrix
- we feed (X, A) into GNN and the GNN performs message passing, meaning the nodes share information with their neighbors
- the output H contains the latent representations (or embeddings) and the Node vector h_i captures both the original features x_i and the structural info about its surrounding neighborhood.

![[Pasted image 20260915004426.png]]

### learning on graph structures





### deep graph layers




### applications of GNNs











## Links:

202609150009
