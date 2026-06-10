---
title: preventing overfitting in nn
draft: false
tags:
  - overfitting
  - batch-norm
  - regularization
  - dropout
  - early-stopping
date: 2026-06-10
description: preventing overfitting in nn - regularization, dropout, early stopping, batch norm
---
# preventing overfitting in nn

notes - https://miro.com/app/board/uXjVIByBwVI=/?share_link_id=231943841648
colab - https://colab.research.google.com/drive/1i-BYQ25nNarpnfLDczXNrNEjZlDYL7tm?usp=sharing

overfitting:
- occurs when the model learns the training data too well including noise and outliers
- it performs poorly on unseen data!

symptoms:
- training loss is low
- validation loss starts increasing after some epochs

methods to overcome overfitting:
- regularization - adding penalty to large weight values - L1, L2 reg as large weights make model very sensitive to change in the input data
- dropout - randomly dropping a fraction of neurons in a layer at each fwd pass
- early stopping - stop training when the model starts to overfit (ie validation performance worsens)
- batch norm - normalizes activations in intermediate layers to zero mean and unit variance (usually done after activation)

![[Pasted image 20260610193040.png]]



## Links:

202606101352
