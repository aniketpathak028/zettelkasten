---
title: multimodal deep learning
draft: false
tags:
  - multi-modal-dl
date: 2026-09-12
description: multi modal deep learning
---
# multimodal deep learning

### what is multi-modality and why is it needed?

- deep learning models may leverage 2 or more modalities - image, text, audio, 3d, video etc
- human perception is multimodal
- applications - VQA, visual and video grounding, autonomous driving etc
- DL models especially transformer based are data hungry so "more modalities = more data"

![[Pasted image 20260912140940.png]]

- healthcare, medical imaging, robotics, virtual assistance, gen AI
- transformers are:
	- model agnostic architectures - everything can be tokenized
	- attention enables cross-modal interactions
	- transformers scale well with data, and can be pre-trained
### multimodal interaction paradigms and effects

- fusion - combines multiple modalities to jointly produce a single, shared output
- coordination - keep per-modality representations separate, but align them with each other
- fission - decomposes a shared representation back into modality-specific outputs

- Multimodal fusion:
	![[Pasted image 20260912143451.png]]

![[Pasted image 20260912143515.png]]

- Fusion combines modalities providing a joint output. 
- Coordination aligns outputs, but each modality still has an individual output, and processing itself may not happen jointly.

- the joint output can be inconclusive, can be dominated by one modality, can be modulate, or we can get emergent info that cannot be derived from either modality independently!
### interaction strategies

- raw or early fusion
	- fusion at raw level or at data level
	- requires the modalities to be homogeneous (otherwise cannot be fused!)
	- ex- fusion of rgb, depth and skeletal data
- output or late fusion
	- make pred for each modality separately and then fuse the pred
	- supports heterogeneous modalities (because each modality is processed separately)
	- ex- avg, voting, highest prob, learning-based etc
- intermediate fusion
	- extract feat for each modality, fuse feat and pred jointly
	- supports heterogeneous modalities
- early fusion - common in transformer based arch where one modality is transformed to match another modality
- hybrid fusion - at diff stages

#### imp to understand the diff

- multimodal fusion - learn a shared representation capturing interactions across modalities, producing a unified output
- multimodal coordination - learn a separate per-modality representation that are aligned with each other ex- used for cross modal retrieval

	![[Pasted image 20260912151632.png|490]]

	![[Pasted image 20260912151745.png|492]]

![[Pasted image 20260912152001.png]]

### feature fusion

![[Pasted image 20260912214533.png]]

![[Pasted image 20260913001946.png]]

![[Pasted image 20260913002246.png]]

![[Pasted image 20260913002407.png]]

- higher order fusion
    - we can already make unimodal + bimodal + trimodal terms using fusion but can we add higher-order interaction terms like - xa^2 + xb^2 etc
    - we could but it would be computationally expensive
    - better way - fuse all features into a single feature vector → f = (1, z1, z2, z3...) and multiply it P times to get P-modal terms → F = f.f.f.f.f… P times
    - ex - if we have a feat vector of 100 feat and we want P=5 we would have 100^5 elements in the matrix which is un-computable hence we never compute it but use a low rank tensor network W to contract it into a smaller more useful matrix Z
    - how can we model highly non-linear interactions?
        - using neural networks by concatenating feat and letting the n/w learn how to fuse them! y’ = f((Xa, Xb,...))

![[Pasted image 20260913003748.png]]

- tensor fusion is a combination of unimodal and bimodal parts, hence combines additive and bilinear fusion
- we can compute an attention weight maybe based on a neural network

### Vision and Language - Early and BERT like models

- early models for vqa used an LSTM to process the text and a CNN to process the image finally having 1024 FC feature representation which was then element wise multiplied (fusion) to predict the final softmax prob!
- FiLM - **Feature wise Linear Modulation** modulated the output of each layer of one modality conditioned on the other modality ex- the text is processed by a GRU type RNN which helps train a gamma and a beta params that are used by the CNN layers
- BERT - **Bidirectional Encoder Representations from Transformers** is used primarily as a text encoder in various NLP tasks and is pre-trained with 2 self-supervised objectives, and fine-tuned on downstream tasks. No human annotated data is needed and it allows for training on vast unlabelled datasets
- extending BERT to vision and language?
	- how to encode images? (Region features, CNN features, linear projection)
	- how to model interactions? (single or dual stream)
- BERT + Vision - VilBERT
	- ViLBERT (Vision and Language BERT) - Region features (Faster RCNN) + Dual stream
	- uses self-attention for unimodal refinement
	- uses cross-modal attention for multimodal interactions - use Q from one modality and V, K from other modality
- BERT + Vision - UNITER
	- UNITER - Universal Image-Text Representation - Region features (Faster R-CNN) + Single stream
	- self attention on concatenated visual and language tokens allows for multi-modal interactions
	- CONS- region feat extractors are slow takes around 900ms, trained on a fixed set of classes and lose all context information
- BERT + Vision - Pixel-BERT
	- replaces region features with CNN features (ResNet or ResNeXt) + Single stream.
	- random sampling of pixels for computation reduction and semantic reasoning.
- BERT + Vision - ViLT
	- ViLT (Vision and Language Transformer) - Linear projection of patches (ViT) + Single stream. Linear projection drastically decreases runtime with similar performance
		![[Pasted image 20260913013354.png]]

![[Pasted image 20260913013405.png|563]]

- The main difference lies in the way the images are encoded and tokenized (region based, CNN, linear proj) and the way multimodal interactions are performed (single vs dual stream)
- we take queries from one modality, keys and values from other modality
- Multimodal masked language modeling, image-text matching



## Links:

202609121311
