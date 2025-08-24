---
title: pod
draft: false
tags:
  - pods
  - k8s
  - kubectl
date: 2025-08-23
---

# pod

`fun fact: the name pod comes from the saying pod of whales!`

- smallest element in a k8s cluster
- a pod is not a container
- a pod is a collection of containers + other resources!
- a pods can have:
	- single container
	- multi container
	- init container: an init container is a container that needs to run successfully for the pod to run. ex- an init container that checks whether a db connection is set (it can be used to do pre checks needed for a pod to run!)
	- Networking
	- Storage


`even though a pods is not a container but the most common pods are single container pods!`


```bash
# runs a pod with a container with nginx image!
kubectl run nginx-aniket --image=nginx 

# definition of the pod - containers, networking storage
kubectl describe pod nginx-aniket

# gets pods in the current namespace
kubectl get pods 

# gets pods in all namespaces
kubectl get pods --all-namespaces

```








## Links:

202508231258