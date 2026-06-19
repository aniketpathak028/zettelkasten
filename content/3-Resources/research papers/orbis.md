---
title: orbis
draft: false
tags:
  - orbis
  - flow-matching
date: 2026-06-17
description: orbis
---
# Orbis - Overcoming challenge of Long-Horizon prediction in Driving World Models

- imagines and generates realistic video of the next frames
- long-horizon generation even in turns and chaotic moments
- favors continuous math over discrete tokens
- single-cam video and basic driving actions - steering, speed
- 469M params only
- trained on only 280 h of video

-> discrete vs continuous
- continuous - images are unbroken numerical values - diffusion models, flow matching
- discrete - image is broken into patches and each patch is a token 

-> hybrid tokenizer

- high res video frame -> encoder -> latent space 
- latent space -> quantizer (turns data into discrete ids) -> Discrete models
- latent space -> continuous vector (keeps data fluid) -> flow matching models









## Links:

202606171509
