---
title: kubectl
draft: false
tags:
  - kubectl
  - k8s
  - cli
date: 2025-08-22
---
# kubectl

- controls the kubernetes cluster manager
- use the --help for learning about any command in kubectl

kubectl commands
```shell
######### context ################

# check current context
kubectl config current-context

# list all contexts
kubectl config get-contexts

# set context
kubectl config use-context rancher-desktop


############ pods ###############

# get pods in the default namespace
kubectl get pods

# list all the namespaces
kubectl get namespaces

# 
```


 

## Links:

[[kubernetes]]

202508221357