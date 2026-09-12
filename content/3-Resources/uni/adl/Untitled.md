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
- DL models especially transformer based are data hungry so more modalities = more data
![[Pasted image 20260912140940.png]]
- healthcare, medical imaging, robotics, virtual assistance, gen AI
- transformers are:
	- model agnostic architectures - everything can be tokenized
	- attention enables cross-modal interactions
	- transformers scale well with data, and can be pre-trained

### multimodal interaction paradigms and effects
- fusion - combines multiple modalities to jointly produce a single, shared output
- coordination - keep per-modality representations separate, but align them with each other
- fission - decompose a shared representation back into modality-specific outputs

- Multimodal fusion:
	![[Pasted image 20260912143451.png]]

![[Pasted image 20260912143515.png]]

- Fusion combines modalities providing a joint output. 
- Coordination aligns outputs, but each modality still has an individual output, and processing itself may not happen jointly

- the joint output can be inconclusive, can be dominated by one modality, can be modulate, or we can get emergent info that cannot be derived from either modality independently!

### interaction strategies

- raw or early fusion
	- fusion at raw level
	- requires the modalities to be homogeneous
	- ex- fusion of rgb, depth and skeletal data
- output or late fusion
	- make pred for each modality separately and fuse the pred
	- supports heterogeneous modalities
	- ex- avg, voting, highest prob, learning-based etc
- intermediate fusion
	- extract feat for each modality, fuse feat and pred jointly
	- supports heterogeneous modalities
- early fusion - common in transformer based arch where one modality is transformed to match another modality
- hybrid fusion - at diff stages
- multimodal fusion - learn a shared representation capturing interactions across modalities, producing a unified output
- multimodal coordination - learn a separate per-modality representation that are aligned with each other ex- used for cross modal retrieval

	![[Pasted image 20260912151632.png|490]]

	![[Pasted image 20260912151745.png|492]]

![[Pasted image 20260912152001.png]]





## Links:

202609121311
