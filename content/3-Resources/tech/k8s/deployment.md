---
title: deployment
draft: false
tags:
  - k8s
  - pods
  - kubectl
date: 2025-08-24
description: the wonders of k8s deployments!
---
# deployment

Note:
`in prod we never run individual pods, we use something called deployment to orchestrate the creation of pods! Deployments are a way to express your desired state for an app to k8s`

### What is the major difference between containers, pods and deployments?

- containers - a single isolated unit that can be run by a single docker command using the docker api, no auto-scaling or auto-healing features present!
- pods - declarative approach by k8s where we just mention the desired state in a yaml file and k8s achieves it! doesn't need a cli based approach but still no auto-scaling and auto-healing capability!
- deployments - a wrapper over pods, as pods are rarely run in deployment, it rolls out replica-sets or controller which always maintains the desired number of pods in the deployment. It ensures auto-scaling and auto-healing features that can be used in production.

![[k8s-deploymenty.png|427]]

![[Pasted image 20260324210502.png|432]]
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

# create a deployment (creates deployment.apps)
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

# more info on replica-sets
kubectl describe replicasets.apps
```

Note:
- when there is any issue in the k8s cluster always check the deployment events with the describe command to get info
- deployments have a default spec.strategy of RollingUpdate
- RollingUpdate means the deployment updates pods in a rolling update fashion (gradually scale down the old ReplicaSets and scale up the new one)
- while the Recreate strategy means all existing Pods are killed before new ones are created

this is how a deployment yaml file looks 👇

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx-depl
  name: nginx-depl
spec:
  replicas: 10
  selector:
    matchLabels:
      app: nginx-depl
  template:
    metadata:
      labels:
        app: nginx-depl
    spec:
      containers:
        - image: nginx
          name: ngingx
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1 # the max no of pods that can be deleted
      maxSurge: 1 # the max number of extra pods that can be created
```


Note:
this basically means telling k8s to achieve the desired state of 10 pod replicase given it can have 1 pod unavailable and 1 extra pod running at any point in time! so, the state can be 9 pods fully available and 1 extra pod at any point in time!

To see the magic of RollingUpdate do the following:

- change the deployment config (maybe use an old image version)
- run the command `watch -n 1 kubectl get pods`
- apply the changed deployment in a window side by side

![[rolling-update.png]]

## Links:

[[pods]]
[[kubectl]]
[[kubernetes]]
[[deploying a simple app using k8s]]

202508242011