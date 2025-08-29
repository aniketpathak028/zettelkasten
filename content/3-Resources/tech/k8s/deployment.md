---
title: deployment
draft: false
tags:
  - k8s
  - pods
  - kubectl
date: 2025-08-24
---
# deployment

Note:
`in prod we never run individual pods, we use something called deployment to orchestrate the creation of pods! Deployments are a way to express your desired state for an app to k8s`

### things to know:

- we can create a deployment just like we create pods using the cli or using yaml
- deployment contains info about the type of pod, replicas etc.
- deployments create a replica-set that actually creates the replicas of the pods
- k8s manages replica-sets for you, and it is not advised to manage it yourself! 

Note:
`k8s tends to keep old replicasets around, so you might see multiple replicasets for the same deployment`

```bash
# learn about deployment
kubectl create deployment -h | less

# create a deployment (creates something like deployment.apps)
kubectl create deployment test --image=httpd

# get more info about the deployment
kubectl describe deployment.apps test

# edit a deployment (not recommended)
kubectl edit depoyments.apps test

# delete a deployment
kubectl delete deployments.apps test

# fetch deployments
kubectl get deployments.apps

# generate yaml for deployment
kubectl create depoyment test --image=httpd --replicas=10 --dry-run=client -o yaml

# get replica set
kubectl get replicasets.apps
```



## Links:

[[pods]]
[[kubectl]]

202508242011