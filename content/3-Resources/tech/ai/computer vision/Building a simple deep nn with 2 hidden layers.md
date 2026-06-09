---
title: Building a simple deep nn with 2 hidden layers
draft: false
tags:
  - neural-networks
  - deep-learning
date: 2026-06-09
description: Building a simple deep nn with 2 hidden layers
---
# Building a simple deep nn with 2 hidden layers

notes - https://miro.com/app/board/uXjVIPXuHKk=/?share_link_id=843762054496
colab - https://colab.research.google.com/drive/1m4JuGfPdqL59SF1X_6lcRT-NEKy4azov?usp=sharing
### problems with the linear layer in the last experiment
- we had a single layer which means we just converted the image (H x W x C) into patches by flattening and used it to predict the class!
- as per the training and validation curves, the model was clearly trying to overfit after a certain number of epochs as the training acc increases and the validation accuracy plateaus and decreases
- the batch size (16), optimizer setting (0.001) - i.e. hyperparam tuning could have been better but this can be done only with trial and error!
![[Bildschirmfoto 2026-06-09 um 10.31.06 AM.png]]
### new model architecture

old model params:
	- hidden layer 1 : 224 x 224 x 3 = 150528
	- output layer : 5
	- number of params : 150528 x 5 = 752640 (trainable params)
new model params:
	 - HL 1 : 224 x 224 x 3 = 150528
	 - HL 2 : 128, activation: RELU
	 - output layer: 5
	 - number of params : 150528 x 128 + 128 x 5
	
### results of the new model
- unlike expected, that the accuracy would increase, it remains almost the same
- while the loss in now lower! this means the model is predicting the class more confidently however the accuracy remains the same because of the other hyperparams like - batch size, LR, image size, EPOCHs etc. and also because it is ultimately a simple nn with only 2 layers!
![[Pasted image 20260609131715.png]]


### Hyperparams vs params:
- params - weights, biases
- hyperparams - batch size, LR, loss func, # hidden layers, epochs, image size
![[Pasted image 20260609132013.png]]
- image size - reducing size can help the model run faster but it loses information that could be useful for the classification task! ex- 224 x 224 -> 64 x 64
- Batch size
 ![[Bildschirmfoto 2026-06-09 um 1.21.07 PM.png]]

![[Pasted image 20260609132157.png]]





### random experiments
![[Pasted image 20260609132341.png]]

- a larger batch size results in a smoother graph without much steep changes!











## Links:

202606091019
