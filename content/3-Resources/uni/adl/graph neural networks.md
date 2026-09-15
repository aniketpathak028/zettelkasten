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

![[Pasted image 20260915004358.png|536]]

X - Node Features, A - Adj Matrix, H - embedding matrix
- we feed (X, A) into GNN and the GNN performs message passing, meaning the nodes share information with their neighbors
- the output H contains the latent representations (or embeddings) and the Node vector h_i captures both the original features x_i and the structural info about its surrounding neighborhood.

![[Pasted image 20260915004426.png]]

### learning on graph structures

- GNN properties:
	- processing should account for the structure of graphs
		- processing should take connectivity into account
		- a node should be influenced by its neighbors
		- there is no canonical order for the nodes of the graph
	- any operation should not depend on the node ordering induced by X
	- we can construct GNN with 2 abstract operations:
		- maps - given node features X, map them to new feat H = f_map(X,A) ex- GNN layers, node-level predictions
		- reductions - given node features X, produce a single output y = f_red(X,A) ex- Graph-level predictions
		- both must not depend on the node ordering induced by X (but how?? - to understand it we need to define what we mean by node ordering)
- Permutations
	- define re-ordering of elements
	- ex- P=(1, 3, 0, 2) and we have a certain order X we can permute it using P.X
	- since the adj matrix A encodes the node connections, we must change it with node permutations also to maintain a consistent graph structure
	- we need to permute both rows and columns ie. Xp = PX => Ap = PAP^T
	- Permutation invariance means that permuting 2 nodes in a graph results in the same output for the operation. Reduction is a permutation invariant operation.
	
	![[Pasted image 20260915014313.png|656]]
	
	![[Pasted image 20260915014339.png]]
	
	- Permutation equivariance means that permuting the order of the node permutes the output in the same order

	![[Pasted image 20260915015758.png]]

	![[Pasted image 20260915015734.png]]

	![[Pasted image 20260915020836.png]]

	![[Pasted image 20260915020852.png]]

	- PointNet are GNNs!

	![[Pasted image 20260915021130.png]]

	- permutation invariance - shuffling the input nodes has 0 effect on the output ie. f(PX, PAP^T) = f(X, A) = y
	- permutation equivariance - shuffling the input nodes causes the rows of the output matrix to shuffle in the exact same order ie. f(PX, PAP^T) = Pf(X, A) = PH
	- we used summation function as an aggregation fn in the deep sets example
### deep graph layers

![[Pasted image 20260915023152.png]]

3 types of GNNs:

![[Pasted image 20260915023209.png]]

- locality in graph layers - a graph layer is called local if every latent h_i depends only on x_i and N_i
	- we only consider graph layers of the form f(X, A) = (H, A)
![[Pasted image 20260915024527.png]]

- Degree matrix is a diagonal matrix containing node degrees Dii
- Graph Laplacian
![[Pasted image 20260915024718.png]]

- Challenges in unnormalized Graph laplacian:
	- Varying Node Degrees - Nodes with highly varying degrees create a wide range of values in the degree matrix D
	- Gradient Instability - The degree variation can cause instability in gradient based methods, with high-degree nodes dominating the learning process
	- Training Instabilities - This variability can lead to gradient explosion or vanishing gradients, disrupting model convergence.
- Therefore we introduce the normalized Graph Laplacian
![[Pasted image 20260915025430.png]]

![[Pasted image 20260915025526.png]]

Interpretation - the normalized graph laplacian provides a measure of the smoothness of a graph representations in a degree aware manner!

![[Pasted image 20260915030054.png]]

> Notice the difference in the different matrices!

- Graph Convolution Networks - GCN
	![[Pasted image 20260915030803.png]]

	![[Pasted image 20260915030914.png]]

	![[Pasted image 20260915031009.png]]

	- How the node gets updated in 1 GCN update step?

	![[Pasted image 20260915031210.png|525]]

	- Stacking multiple GCN layers:
	![[Pasted image 20260915031542.png]]

	- Node classification example
	![[Pasted image 20260915031754.png]]

	- GCN - Generic Formulation
	![[Pasted image 20260915031948.png]]

> If the aggregation weights cij depended on the feat xi and xj it would be a Graph Attention Network!

![[Pasted image 20260915032338.png]]

![[Pasted image 20260915032403.png]]

How the attention mechanism works in GAT?
![[Pasted image 20260915032638.png]]
- a shared weight matrix is used to project x_i and x_j which are then concatenated
- then we dot product the concatenated vector with a learned attention vector and take a Leaky RELU
- finally we take the softmax of the attention scores
![[Pasted image 20260915032904.png]]

- Message passing neural networks - MPNNs
	- generalized framework for GNNs
	- introduces learned vectors (called messages) that propagate across edges
	- can incorporate edge features for enhanced expressiveness
	- Challenges - scalability and learnability issues on large or complex graphs
- MPNNs decompose the fwd pass into 2 main phases:
	- message update - uses a message function to compute messages across edges
	- node update - update node embeddings using a vertex update function
- message passing process - at each layer l 
	- decomposes into 2 operations:
		- node-to-edge operation (v->e)
		- edge-to-Node operation (e->v)
	- incorporates node and edge features to generate updated representations

![[Pasted image 20260915125317.png]]

![[Pasted image 20260915125440.png]]

![[Pasted image 20260915125711.png]]

- Graph Pooling Layers
	- sometimes we may need to reduce the nodes in a graph ex- graph classification with one single node representing the whole graph
	- for this we need Graph pooling layers
	- pooling types 
		standard- sum(), mean(), max(), min()
		cluster based - differentiable pooling

- Top-k-pooling
	- Graph U-nets - Hierarchical Graph classifiers
	- Self-attention pooling - SAGPool, understanding attention and generalization in GNNs
	- Edge Pooling
	- Differentiable Pooling

![[Pasted image 20260915130608.png]]
- using node degrees, specifically we define Ã = D^-1/2 A D^-1/2
- self loops and skip connections
- the number of cluster param is a hyperparam, chosen by us or needs to be specified through some heuristic
### applications of GNNs
- point cloud classification and segmentation
- traffic forecasting
- scene graph generation
- 3D multi object tracking
- recommender systems
- drug discovery
- there is more - medical diag, spread of covid, particle physics etc


### further topics
- node embeddings
- page-rank algorithm
- deep graph clustering
- deep generative graph
- spatio-temporal graph neural networks
- adversarial attacks on graphs
- reasoning over knowledge graphs

![[Pasted image 20260915171040.png]]

- GNNs are used to encode molecular structures by modeling atoms as nodes and their bonds as edges. This helps in understanding angle relationships, optimizing distances for stability, predicting molecular properties (such as freezing points or acid/base behavior) and is foundational to breakthroughs like DeepMind's AlphaFold for modeling protein structures.
- Relying purely on visual similarity is often ineffective because objects can look very similar but fulfill completely different functions (lacking recommendation diversity). A GNN approach encodes textual features and learns attention weights over a product graph, enabling the system to recommend items that are functionally relevant and diverse, rather than merely visually identical.

## Links:

202609150009
