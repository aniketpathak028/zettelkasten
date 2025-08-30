---
title: pod
draft: false
tags:
  - pods
  - k8s
  - kubectl
date: 2025-08-23
description: learn about k8s pods and how they work?
---
# [pod](https://kubernetes.io/docs/concepts/workloads/pods/)

`fun fact: the name pod comes from the saying pod of whales, and the entire k8s ecosystem is based on nautical terms. Even Kubernetes is a greek word which means a helmsman who orchestrates the ship, analogous to how k8s orchestrates pods!`

![[content/assets/pod-of-whales.png]]

## things to know

- a pod is the smallest element in a k8s cluster
- a pod is not a container!
- a pod is a collection of containers + other resources!
- a pod can have:
	- single container
	- multi container
	- init container: an init container is a container that needs to run successfully for the pod to run. ex- an init container that checks whether a db connection is set (it can be used to do pre checks needed for a pod to run!)
	- Networking
	- Storage

Note:
`even though a pods is not a container but the most common pods are single container pods!`

Pod related commands:
```bash
# runs a pod with a container haivng nginx image!
kubectl run nginx-aniket --image=nginx

# definition of the pod - containers, networking storage
kubectl describe pod nginx-aniket

# gets pods in the current namespace
kubectl get pods 

# gets pods in all namespaces
kubectl get pods --all-namespaces
```

more on [[interacting with pods]]
## Links:

[[interacting with pods]]
[[kubernetes]]
[[kubectl]]

202508231258