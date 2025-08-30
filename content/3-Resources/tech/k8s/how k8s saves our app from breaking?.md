---
title: how k8s saves our app from breaking?
draft: false
tags:
  - k8s
  - deployment
date: 2025-08-30
description: understand how k8s saves businesses
---
# how k8s saves our app from breaking?

today I learned a wonderful feature about k8s, which is how it saves our app from crashing when we have a container error.

for example if we have the below deployment 👇
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
        - image: nginx:1.28.0-alpine3.21
          name: ngingx
          command: ["/bin/bash", "-c"] # override the default command
          args: ["sleep 5; exit 1"] # sleep for 30 s then exit with an error
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1
      maxSurge: 1
```

the command in the yaml file forces the containers to exit with code 1 causing container error!

k8s is smart enough to handle this efficiently instead of rolling out the change further to other pods, once it detects the error caused in the first rolling change, it goes into CrashLoopBackOff and doesn't propagate the change further saving our app from crashing!

![[container-error.png]]

how amazing piece 😇 of tech ain't it? 

202508302258