---
title: deploying an app using k8s
draft: false
tags:
  - k8s
  - deployment
date: 2025-08-31
description: how to deploy an app in k8s?
---
# deploying a simple app on k8s

in this tutorial I share my understanding on deploying a simple application like [mealie](https://github.com/mealie-recipes/mealie) using k8s

step-1: create a namespace for the app - [[namespaces]]

step-2: create a deployment in the namespace

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: mealie
  name: mealie
  namespace: mealie
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mealie
  template:
    metadata:
      labels:
        app: mealie
    spec:
      containers:
        - image: ghcr.io/mealie-recipes/mealie:v1.2.0
          name: mealie
          ports:
            -containerPort: 9000
```
specify the container image with the version and expose a port!

step-3: switch to the namespace `k config set-context --current --namespace=mealie`

```bash
❯ kubectl get pods
NAME                      READY   STATUS    RESTARTS      AGE
aniket                    1/1     Running   1 (45m ago)   8h
mealie-5479dbb894-8v5wd   1/1     Running   0             114s
❯ kubectl get deployments.apps
NAME     READY   UP-TO-DATE   AVAILABLE   AGE
mealie   1/1     1            1           119s
```

step-4: forward local port to pod for accessing the app

```bash
❯ kubectl port-forward pods/mealie-5479dbb894-8v5wd 9000
Forwarding from 127.0.0.1:9000 -> 9000
Forwarding from [::1]:9000 -> 9000
```

step-5: go to `localhost:9000` on your browser and your app would be up and running! 🎉

step-6: incase we want to update the application using a new image (ex- say the latest one), we can change the image in the deployment.yaml file and apply it using the RollingUpdate strategy to avoid any downtimes.

```bash
kubectl apply -f deployment.yaml
```

Note:
there are better ways to host an app without port forwarding and with persistence - [[k8s services]]



## Links:

[[deployment]]
[[kubernetes]]
[[k8s services]]

202508311055