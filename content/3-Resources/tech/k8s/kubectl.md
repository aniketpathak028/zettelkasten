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

- cli tool to interact with the k8s cluster.
- controls the kubernetes cluster manager

The format of kubectl command is:-
`kubectl [action] [resource] [name] [flags]`
- action - operation to perform - get, create, apply, delete, describe, logs, exec
- resource - type of k8s object - pod, node, namespace, service, deployment
- name - optional
- flags - optional - (-n) or (-o)

```shell
# check current context
kubectl config current-context

# list all contexts
kubectl config get-contexts

# set context
kubectl config use-context rancher-desktop

# get pods in the default namespace
kubectl get pods
kubectl get pods -n <namespace>

# list all the namespaces
kubectl get namespaces

# create and run an image in a pod
kubectl run <podname> --image=<image>
```

 
## Links:

[[kubernetes]]

202508221357