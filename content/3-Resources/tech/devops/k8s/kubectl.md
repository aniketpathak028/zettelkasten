---
title: kubectl
draft: false
tags:
  - kubectl
  - k8s
  - cli
date: 2025-08-22
description: what is kubectl?
---
dock# kubectl

- cli tool to interact with the k8s cluster.
- controls the kubernetes cluster manager

The format of kubectl command is:-
`kubectl [action] [resource] [name] [flags]`
- action - operation to perform
	- get
	- create
	- apply
	- delete
	- edit
	- describe
- resource - type of k8s object
	- pods
	- nodes
	- svc
	- deployments
	- namespaces
- name - optional
- flags - optional (-n) or (-o)

```shell
# view the current config
kubectl config view

# check current context
kubectl config current-context

# list all contexts
kubectl config get-contexts

# set context
kubectl config use-context rancher-desktop

# get pods in the default namespace
kubectl get pods

# get pods in a specific namespace
kubectl get pods -n <namespace>

# get nodes
kubectl get nodes

# list all the namespaces
kubectl get namespaces

# create and run an image in a pod
kubectl run <podname> --image=<image>
```

## Links:

[[kubernetes]]

202508221357