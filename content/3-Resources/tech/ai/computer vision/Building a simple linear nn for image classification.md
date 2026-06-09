---
title: image classification with a simple nn
draft: false
tags:
  - neural-networks
  - image-classification
date: 2026-06-06
description: image classification with a simple nn
---
# image classification with a simple nn

notes link - https://miro.com/app/board/uXjVIPolTio=/?share_link_id=225966248894
colab - https://colab.research.google.com/drive/15D91NChzSrEM2kTr9E8GI6l1FGvu6men?usp=sharing

### architecture of our nn
- here we build a shallow nn with no activation fn to see how well it can perform in image classification 
> as a general concept, the model should atleast perform better than 20% accuracy as a random guesser would still have 20% acc because there are 5 classes

- classes - daisies, dandelions, roses, sunflowers, tulips
- each pic is jpeg and each category has 1000 images
- image processing : load -> jpeg to rgb -> scale 0-1 -> resize 224 x 224 x 3
- batch dim img -> 16 x 224 x 224 x 3, label -> 16 (labels are turned into numbers for each class 0-4)
- architecture - flattening -> dense FC -> softmax

### results of the experiment

![[Pasted image 20260609135343.png]]

![[Pasted image 20260609135315.png]]

### how to improve?
- use deep nn with more hidden layers
- use non-linear activation
- use convolution operation




## Links:

202606051832
