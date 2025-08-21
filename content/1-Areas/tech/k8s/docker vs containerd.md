---
title: docker vs containerd
draft: false
tags:
  - docker
  - containerd
  - k8s
date:
---
# docker vs containerd

History of docker and k8s:
- k8s was mainly supporting docker as container runtime
- however other vendors like rocket needed k8s support too!
- so, k8s built this interface called CRI (container runtime interface) which helped k8s run other container runtime as long as they followed the OCI (open container initiative)
	- OCI (imagespec and runtimespec)
	- although this helped other container runtimes to use k8s but the fun fact was docker was not compatible with CRI! 
	- so k8s introduced something called dockershim to continue support for docker! (it was sort of a hack to bypass docker from using CRI)
- Docker too contains several tools put together ex-
	- cli, api, build, volumes, auth, security and containerd
	- containerd is CRI compatible and thus docker could be run by containerd instead of dockershim now and its support by k8s was remved in v1.24!
- now containerd contains [[cli-nerdctl]] and [[cli-ctr]] to manage runtimes
- while k8s has its own tool called [[cli-crictrl]]


## Links:

[[containerd]]

202508211938