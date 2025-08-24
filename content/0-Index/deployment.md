---
title: deployment
draft: false
tags:
  - k8s
  - pods
  - kubectl
date: 2025-08-24
---
# deployments

`in prod we never run individual pods, we use something called deployment to orchestrate the creation of pods! Deployments are a way to express your desired state for an app to k8s`

- we can create a deployment just like we create pods using the cli or using yaml
- deployment contains info about the type of pod, replicas etc.
- deployment 

```bash

# learn about deployment
kubectl create deployment -h | less

# create a deployment (creates something like deployment.apps)
kubectl create deployment test --image=httpd

# edit a deployment (not recommended)
kubectl edit depoyments.app test

# delete a deployment
kubectl delete deployments.app test

# generate yaml for deployment
kubectl create depoyment test --image=httpd --dry-run=client -o yaml



```





## Links:

202508242011