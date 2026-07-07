---
title: flow matching
draft: false
tags:
date:
description: flow matching
---
# flow matching

paper - https://arxiv.org/abs/2210.02747

-> traditional diffusion models
- add noise to image step by step until it is gaussian 
- reverse the noise in the image in the same order of steps to learn how to reconstruct the original image
- train a network for each denoising step t=n to t=n-1

-> flow matching (does not define a fixed noising process!)
- proposes that we can learn to generate the original dist (data) from a random gaussian noise with only samples from that dist
- since we do not know the final dist, we use the gaussian of all our samples or the empirical distribution (ie. the uniform mixture of these exact points)

-> the flow matching trick
- since flow matching cannot find a vector field that maps a global noise distribution to a completely unknown global data distribution all at once. 
- it simplifies it by using conditional flow matching, so instead of mapping to  the entire distribution q, it learns to map to a specific data point at a time and since this distribution is already known, the model can easily recreate it from noise, and training it on millions of such samples, the model learns the complex global structure of q.
- it can be shown that if the model learns to transform gaussian noise into single sample distributions individually, aggregating it for all the samples will allow it to do the same for any distribution!

![[Pasted image 20260617190301.png|318]]

![[Pasted image 20260617185829.png]]

- at every step we 


## Links:

202606171828
