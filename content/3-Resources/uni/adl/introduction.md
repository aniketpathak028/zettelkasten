---
title: introduction to deep learning
draft: false
tags:
  - dl
date: 2026-09-16
description: introduction to deep learning
---
# introduction

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



## Links:

202609161125
