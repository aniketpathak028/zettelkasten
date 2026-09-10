---
title: transfer learning and domain adaptation
draft: false
tags:
  - transfer-learning
  - domain-adaptation
date: 2026-09-06
description: transfer learning and domain adaptation
---
# transfer learning and domain adaptation

### why?

- traditional DL:
    - isolated for separate tasks
    - needs large data
    - comp expensive
    - models are static after training
- challenges:
    - poor performance with limited data - overfitting / under-fitting / poor generalization
    - poor domain transfer - model for one domain performs bad in other domain
    - evolving data - changes in env results in model’s degradation
- the vicious cycle:
    - annotated data → model depl → model obsolete → data collection → annotated data
    
![[Pasted image 20260909161140.png]]
- poor performance with limited data
- lacking domain transfer
- evolving data landscapes

### transfer learning

- reusing the knowledge from a pre-trained model to solve a new task!
- step-1 - pretrain the model on a related task with lot of data ex- AlexNet
- step-2- apply to target task - feat extraction or fine-tuning
    - feat-extraction - frozen model + trainable head
        - use pre-trained model to extract generic feat
        - train n/w on top of the model called head on the target task using these feat
        - ideal when the target data is very limited
    - fine-tuning - partially trainable model + fully trainable head
        - train the pre-trained model on the specific target task
        - apply past knowledge from src and relearn the target domain
        - ideal when the target data is large
- transferable knowledge - info, patterns, representations
- types of transferable knowledge
    - low level feat
        - edges, color, word embedding
        - fundamental characteristics
    - high level semantics
        - abstract and complex concepts
        - images - recognizing obj or context
        - text - understanding sentiment
    - domain specific
        - specific to a particular domain → improves performance on same task
    - generic knowledge
        - not specific to a particular task → can be transferred to a wide range of tasks and domains
        - ex - ImageNet pre trained model - semantic seg, depth est, pose est
    - high task sim
        - ex - truck recog and car recog
    - low task sim
        - ex - speech recog and obj det
    - high domain sim
        - dataset with similarity
    - low domain sim
        - distinct datasets
- when to use transfer learning?
    - insufficient data
    - limited compute
    - time constraints
- efficient fine tuning techniques
    - quantization - quantize model wt to lower precision for more efficiency!
	- Low-rank adaptation (LoRA) - freeze the original model wt and instead train so called rank decomposition matrices
    - QLoRA - quantization + low rank adaptation

![[Pasted image 20260909170522.png]]

![[Pasted image 20260909171930.png]]

![[Pasted image 20260909171944.png]]

- initially A is a gaussian dist and B=0 making delta BA=0
- The idea is essentially breaking down the larger d x d weight matrix into smaller matrices d x r and r x d so that the number of params that need update reduces!

- initially without LoRA we need to update ⇒ d x d params
- with LoRA we need to update ⇒ d x r + r x d << d x d when r is a small number!

![[Pasted image 20260909172421.png]]

![[Pasted image 20260909172531.png]]

- Yes, since the domain is the same ie. medical images we can use the pre-trained model to imporve performance
- No, this will very unlikely help as there is low domain similarity

> questions like these in exam! - scenario based

### types of transfer learning

- inductive transfer learning
- transductive transfer learning
- unsupervised transfer learning

- inductive
	- labeled target
	- domain - same, task - diff
    - multi-task learning
	    - labelled src + target
	    - simultaneously learns many tasks and generalizes well
    - self-taught learning
	    - unlabeled src, labelled target
	    - src and target task may be diff
    - ex- pre trained BERT for sentiment analysis, pre trained AlexNet for img segmentation
    - benefits
        - reduces need for large labeled dataset for target task
        - speeds up training process
- transductive
	- labeled src
	- domains - diff, task - same
    - ex- sentiment analysis in english → french, synthetic → real data
    - benefits:
        - allows use of models in new domain without labeled data
        - enhances generalization
- unsupervised transfer learning
	- no labels in src and target
    - ex- [[autoencoders]] , clustering, metric learning
    - reduces need for extensive labels, saving time and resources, improves generalization

how to remember?
![[Pasted image 20260909194049.png]]

> exam tip:- determine task, domain similar, and which learning to use?

![[Pasted image 20260910004404.png]]

- transductive learning - labelled src and unlabelled target, domains diff but sim task ex- sentiment analysis in english -> unlabelled french data!
- self-taught - labelled target but unlabelled src data

### domain adaptation
- problem - src domain and target domain can differ in dist called domain shift and we must try to reduce this gap!
- solution - domain adaptation improves performance on target domain from src domain for the same task by reducing domain shift
- types:
	- unsupervised (transductive) - labelled src domain and unsupervised target domain
	- semi-supervised - some labelled data for target
	- supervised - inductive
- unsupervised - src and target has some overlap
	- problems - src is biased towards src dist and does not perform well in target - poor generalization and overfitting! aka sample selection bias
	- solutions:
		1. importance sampling
			- works when src sufficiently covers target domain
			- give more imp to examples that represent target domain and low imp to ones representing src domain
			- train a binary classifier c to discriminate between src and target data
			- compute importance weight w(x) = (1-c)/c
			- reweight or resample the src data according to w(x)
			- train the task classifier using the reweighted or resampled data
		2. feat alignment - Domain Adversarial Network
			- incase src does not cover target dist
			- the encoder encodes src data and target data
			- we try to fool a domain classifier c -> if the samples are indistinguishable to the discriminator then the dist are aligned
			![[Pasted image 20260910013828.png]]

		- 2 ways to update the domain classifier:
			- gradient reversal
				- acts as an identity function in fwd pass
				- in bwd pass multiplies the gradient by a neg scalar
				- feat extractor produces indistinguishable features for the domain classifier
				![[Pasted image 20260910014707.png]]
			- optimize for 50-50 guessing
				- optimize the feat extractor to make the domain classifier output probabilities close to 0.5 for both src and target domains
				![[Pasted image 20260910122003.png]]
				- this forces the feat extractor to produce feat that the domain classifier cannot distinguish, aligning the source and target feature distributions.
		- advantages:
			- simple to implement and can work well
			- does not require src data dist to cover target data dist
		- disadvantages:
			- requires clear alignment (if the src and target are very different dist, finding a common representation may be difficult or harmful aka negative transfer)
		3. Transferring domain style
			- when it is hard to align feat translate between domains ie. learning a mapping function F (that maps src samples to target samples) and a function G (that maps target samples to source samples)
			- 
		




## Links:

202609061123
