---
title: k8s storage
draft: false
tags:
  - k8s
  - storage
date: 2025-09-12
description: how does k8s persist data?
---
# How to make k8s persist data?

Note:
- a container is ephemeral, ie. it doesn't store any data/state, so once it is deleted, state/data of the container gets lost!
- so in order for a container to store data, it needs to have a volume or a disk mounted to it, which usually happens outside the container.
- the volume is just a piece of the file system where the container is hosted, ex- a piece of the local storage, or it can be provisioned in the cloud.

![[container-volumes.png]]
- consider a volume as an external disk connected to a container for storing data!

### how to create a volume?

read https://kubernetes.io/docs/concepts/storage/volumes/
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-storage
spec:
  containers:
    - image: nginx
      name: nginx
      volumeMounts:
          - mountPath: /scratch
            name: scratch-volume
  volumes:
    - name: scratch-volume
      emptyDir:
        sizeLimit: 500Mi

```

- the volumes are at the pod level and not in the container level, which means they can be used by any container within the pod.
- also the volumes can be pre created or dynamically created during the life cycle of the pod
- note the type of the volume is emptyDir, which is a type of volume in k8s which means it will be deleted when the pod is deleted and it can be used as a temp storage in between containers
- 


## Links:

202509122352