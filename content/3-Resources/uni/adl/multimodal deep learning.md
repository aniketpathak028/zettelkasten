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
- BERT + Vision 
	- ViLBERT
		- ViLBERT (Vision and Language BERT) - Region features (Faster RCNN) + Dual stream
		- uses self-attention TRM for unimodal refinement
		- uses cross-modal attention Co-TRM for multimodal interactions 
			- use Q from one modality and V, K from other modality
	 - UNITER
		- UNITER (Universal Image-Text Representation) - Region features (Faster R-CNN) + Single stream
		- self attention on concatenated visual and language tokens allows for multi-modal interactions
		- CONS- region feat extractors are slow takes around 900ms, trained on a fixed set of classes and lose all context information
	- Pixel-BERT
		- replaces region features with dense CNN features (ResNet or ResNeXt) + Single stream.
		- random sampling of pixels for computation reduction and semantic reasoning.
	- ViLT
		- ViLT (Vision and Language Transformer) - Linear projection of patches (ViT) + Single stream. 
		- Linear projection drastically decreases runtime with similar performance.
		- modal-type embeddings for separate modals
		
		![[Pasted image 20260913013354.png]]

- Pre-training objectives - How to train a Vision BERT model?
	- Multimodal MLM objective - randomly mask tokens and predict them with the aid of unmasked text and visual tokens
	- Image-Text Matching - predict if the sentence and the image are related

![[Pasted image 20260913013405.png|563]]

- The main difference lies in the way the images are encoded and tokenized (region based, CNN, linear proj) and the way multimodal interactions are performed (single vs dual stream)
- we take queries from one modality, keys and values from other modality
- Multimodal masked language modeling, image-text matching

### Vision and Language - Contrastive and Generative Models

- Can we model multimodal interactions without any fusion layer?
	- yes using Contrastive Learning (multimodal coordination) by aligning the feat representations in a shared representation space aka joint embedding space
- CLIP - Contrastive Language Image Pretraining
	- combination of GPT2 for texts and ViT or ResNet for images
	- Large training dataset - new dataset with 400M (image, text) pairs, compared to 15M of previous datasets
	- trained with contrastive loss - InfoNCE due to which it can classify images into classes that were never used during training
	- inference - zero-shot image classification (calculates cosine sim btw image embeddings and all candidate text label embeddings)
	- generalizes much better than ResNet101 on various kinds of datasets like ImageNet-R, ImageNet-A etc.
- FLAVA - combines contrastive and masked pre-training
	- input -> image-text pairs, unpaired images, unpaired text
	- multi-domain joint pre-training - global contrastive, MMM, MIM, MLM
	- output -> Visual recognition, Language understanding, Multimodal reasoning
- SimVLM - Simple Visual Language Model
	- generative
	- PrefixLM loss - given an image and the start of a sentence, predict how to continue the sentence (similar to autoregressive models)
- Flamingo
	- Frozen vision encoder (CLIP) used to modulate a frozen LLM
	- the adapters are trained using a gated cross attention generative loss
	- the overall system is trained using auto-regressive training objective

How modern VLMs work?

- Pre-trained image encoder (often CLIP) - possibly frozen
- visual feat -> (proj layer or image tokenizer) -> tokens that can be processed by language model
- decoder only single-stream transformer trained using a generative loss

Lessons:
- image encoder has the highest impact
- number of visual tokens and image resolution matters more while the type of VL connector has little effect
- careful mixture of captioned images, interleaved image-text and text-only data required to balance multimodal and text-only performance

![[Pasted image 20260913204359.png]]

advantages of contrastive cross-modal pre-training:
- strong 0 or few-short capabilities
- can align representations without explicit fine-grained labels (or pre-training)
- modularity - we can employ already pre-trained encoders and use additional unimodal data for training

advantage of including unimodal training data in multimodal models:
- we are not restricted to aligned pairs - we can leverage significantly more training data and scale model more easily
- large unimodal datasets often cover broader domains and dist than paired multimodal datasets
- additional unimodal data can acts as a form of regularization and improve generalization

### Beyond images and text - Towards Arbitrary Modalities

- VideoBERT
	- similar to Visual language BERTs
	- pre-trained frozen video encoder + BERT (Single stream)
	- large dataset - 23000 hrs of youtube cooking videos
	- text extractor with automatic speech recognition
	- language and video masked modelling + video-text matching
	- tasks - action classification, text-to-video generation, future forecasting 
- Video, Language, Audio - VATT
	- tokenize raw input using linear projections
	- contrastive learning - compare cosine similarity between paired inputs in intermediate video-audio and video-text common space
	- DropToken - randomly drop tokens for reduced computation
- UniT3D - Point cloud and Language
	- 3D region-based extractor for point cloud, and BERT for text, both frozen
	- single-stream transformer decoder for multimodal fusion
	- supervised training - grounding, classification, and text generation
- Multimodal DETR
	- input fusion - attach image info (Color or Feature) to each point
	- intermediate fusion - extract features separately, convert them in a common frame - 3D, Bird's Eye View, or Perspective View and fuse them
	- object query fusion - queries are first refined using one modality and successively using the other modality. No need to convert feat in a common frame ex- CMT - Cross modal transformer
	- CMT - object query fusion for camera and LiDAR
		- avoid sequential decoders by including both BEV and PV projection of object queries' 3D position during positional encoding (PE) step
	- OneLLM - One model to rule them all
		- combines frozen encoder (CLIP) and frozen LLM with modality specific tokenizers and unified proj module to support eight different modalities with a single model
		- challenge - due to the greatly unbalanced dataset OneLLM is trained in multiple stages on the X-text alignment task - Stage 1 (image), Stage 2 (video, audio and point cloud), and stage 3 (depth, normal map, IMU and fMRI)
		- examples from prev stages are included to avoid catastrophic forgetting
	- Multi-Modal graph learning
		- multi-modal graph learning is an instance of heterogeneous graph learning.
		- The main challenge is how to connect multiple modalities with one another to form meta graphs that abstract while still being descriptive wrt the original modality

![[Pasted image 20260913223156.png]]

- by using classical input fusion (via projection) or intermediate fusion
- object-query fusion - fuse on object level via query and adapted decoder transformer

- use multi-stage training strategies

- drop tokens randomly like VATT (or use a more efficient transformer from lecture 3)

### applications
- RT-2-X is a BERT+Vision-style model that processes robotic observations with task instructions to predict the next action. RT-2-X  is trained on (a subset) of Open X-Embodiment
- CrossCLR is a clip style contrastive learning for a video and language cross-modal representation. Improves negative mining to ignore false negatives
- AdapNet++ fuses feat map from modality-specific streams at different layers. self-supervised model adaptation (SSMA) fusion block concatenates the feat maps and re-weights them using an attention mechanism
## Links:

202609121311
