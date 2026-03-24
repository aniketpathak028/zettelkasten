---
title: interacting with pods
draft: false
tags:
  - pods
  - k8s
  - yaml
date: 2025-08-24
description: learn to interact with pods
---
# interacting with pods

- everything in k8s is a yaml file, so are pods
- we can use several commands to interact with pods like - creating, deleting and editing pods
- we can also get inside a pod and do stuff - like ping other pods, checkout the file system of the pod, checkout the activity of the os and more!

```bash
# list pods with more info
kubectl get pods -o wide

# get all pods with all namespaces - shorter
kubectl get pods -o wide -A

# type this to get lots of yaml! 
# it is the pod definition that lives in the cluster
kubectl get pods nginx-aniket -o yaml

# edit pod (not recommended in prod or dev cluster)
kubectl edit pods nginx-aniket

# dry run client to get yaml (imp)
kubectl run nginx-yaml --image=nginx --dry-run=client -o yaml

# output yaml to a file to get started
kubectl run nginx-yaml --image=nginx --dry-run=client -o yaml > nginx-yaml.yaml

# creating/applying a pod definition
kubectl create -f nginx.yaml # only creates the pod
kubectl apply -f nginx.yaml # checks the differences and applies the same

# delete a pod
kubectl delete pod nginx-aniket

# get into a pod and open a shell!
kubectl exec -it nginx-aniket -- /bin/bash

# debug a pod - 2 commands
kubectl describe pods <pod-name>
kubectl logs <pod-name>
```

> Note:
> dry-run
   - none-> default
   - client-> only generates yaml!
   - server-> generates yaml and also runs it!
   

## Links:

[[kubernetes]]
[[pod]]
[[kubectl]]

202508241224