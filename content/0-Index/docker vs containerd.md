---
title: docker vs containerd
draft: false
tags:
date:
---
not really clear with the entire concept yet but here is my understanding:

History of docker and k8s:
- k8s was mainly supporting docker as container runtime
- however other vendors like rocket needed k8s support too!
- so, k8s built this interface called CRI (container runtime interface) which helped k8s run other container runtime as long as they followed the OCI (open container initiative)
	- CRI --> OCI (imagespec and runtimespec)
	- although this helped other container runtimes to use k8s but the fun fact was docker was not compatible with CRI! 😆
	- so k8s introduced something called dockershim to continue support for docker! (it was sort of a hack to bypass )




## Links:

202508211938