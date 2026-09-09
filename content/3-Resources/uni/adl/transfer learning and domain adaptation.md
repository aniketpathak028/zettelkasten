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
- the cycle:
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






## Links:

202609061123
