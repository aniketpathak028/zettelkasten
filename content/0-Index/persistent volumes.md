---
title: k8s persistent volumes
draft: false
tags:
  - k8s
  - k8s-volumes
date: 2025-09-19
description: learn how to persist data in k8s using persistent volumes!
---
## How to persist volumes in k8s?

read - https://kubernetes.io/docs/concepts/storage/persistent-volumes/

### things to know
- persistent volume is like a huge disk running in the cluster
- while persistent volume claim is like a small piece of the persistent volume claimed by an application in the cluster
- volumes are just like any other k8s resource like pods, nodes, etc.
- can be provisioned beforehand or dynamically


### how to create a persistentvolumeclaim?

storage.yaml
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mealie-data
  namespace: mealie
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
```

deployment.yaml
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
        - image: ghcr.io/mealie-recipes/mealie:v3.1.2
          name: mealie
          ports:
            - containerPort: 9000
          volumeMounts:
            - mountPath: /app/data
              name: mealie-data
      volumes:
        - name: mealie-data
          persistentVolumeClaim:
            claimName: mealie-data
```

- once a persistent volume is created and a persistent volume claim is made in the deployment, even if we delete the pods, the data is going to persist
## Links:

[[k8s storage]]

202509192233