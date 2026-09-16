---
title: introduction to deep learning
draft: false
tags:
  - dl
date: 2026-09-16
description: introduction to deep learning
---
# introduction

### Multilayer perceptron

- perceptron is a linear combination of its inputs x plus a non-linear activation function g with learnable params w and b 
- an MLP is a neural net which is:
    - feed fwd (no recurrent conn.)
    - fully connected
    - no of hidden layers = depth
    - no of neurons in hidden layer = width
- activation functions are imp as they are non linear and help the network learn the patterns in the data by helping to propagate gradients in back-propagation, which helps the network minimize the cost function.
- types of activation functions
    - sigmoid - squashes between 0-1, non linear, but vanishing gradient problem, early layers do not learn anything meaningful!
    - ReLU - non linear, solves vanishing gradient but for -ve values the gradient is 0 which is problematic
    - tanH - squashed btw -1 to 1, only useful when targets in that range, 0 centered more balanced
- more activation fn - LeakyReLU, ELU, SELU etc.
- vanishing gradient - occurs when gradients shrink exponentially towards zero during backpropagation in deep neural networks, freezing the weights in earlier layers and halting learning

![[Pasted image 20260916120903.png]]

- no activation function - as regression must output a continuous value with no bounded range, so we don’t want to squash the output!
- with bias = 3 * 5 + 5 * 5 + 5 * 2 + 5 + 5 + 2 = 62
- without bias = 50

### Training and Backpropagation

- loss functions are necessary for the network to minimize the error of the model
- for regression: 1) MAE - L1 loss, 2) MSE - L2 loss, 3) Huber loss = smooth L1
- for classification: 1) Binary classification - logistic loss, 2) Multi-class - cross entropy loss!
- softmax - ensure that the predictions sum to 1
- weights in a neural network are updated using Gradient Descent so we minimize the loss in the negative direction of the gradient!
- w_next = w_old - n * dL/dw_old
- where n is the learning rate and dL/dw_old is the gradient of the loss wrt wt!
- for a convex problem, it is very easy to converge to the optimal weights, but for a real network involving many params, and weights, often the problem in non convex, then we use optimizers like Adam and concepts like momentum to tackle local minima!
- in backprop, the derivative of the loss is calculated wrt every node and every weight in the previous layer and in the process the pre calculated gradient from the subsequent layer is used as per chain rule! this helps the network to minimize the weights to reach the optimal solution!

![[Pasted image 20260916121306.png]]

- when too high - Overshoots minima, loss oscillates or diverges
- when too low - Converges very slowly, may get stuck in local minima

![[Pasted image 20260916121334.png]]

- L2 = (y-y’)^2 ⇒ dL/dy’ = 2(y-y’)

### Recurrent Neural Networks

- recurrent nets allows for cycles which helps retain useful info for sequential data!
- sequence mapping
    - one to many - image captioning,
    - many to one - sentiment analysis, audio sentiment analysis
    - many to many - video frame classification, machine translation, audio translation
- RNN - unfolding, trained using BPTT on the unrolled computational graph

![[Pasted image 20260916121618.png]]

![[Pasted image 20260916121806.png]]

![[Pasted image 20260916121815.png]]


## Links:

202609161125
