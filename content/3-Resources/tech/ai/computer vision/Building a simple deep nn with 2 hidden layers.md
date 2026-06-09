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
- as per the training and validation curves, the model was clearly trying to overfit after a certain number of epochs as the training acc increases and the validation accuracy decreases
- the batch size (16), optimizer setting (0.001) - i.e. hyperparam tuning could have been better but this can be done only with trial and error!
![[Bildschirmfoto 2026-06-09 um 10.31.06 AM.png]]




## Links:

202606091019
