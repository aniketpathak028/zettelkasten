---
title: Untitled
draft: false
tags:
date:
description:
---
# configmaps and secrets

> As per K8s docs - A ConfigMap is an API object used to store non-confidential data in key-value pairs.

### why is configmap needed?

- In most applications we always need to store some sort of data for the application to run for example, if the application uses the database, it might need a database connection path and a port number!
- storing these data inside the application code is non an efficient solution as if any of these change in the future, we might need to manually change them in every container inside the pod.
- Usually it is preferred to store these kinds of information in an env file which can then be accessed by the file system. However k8s offers a better solution to tackle this problem by allowing a resource like configmap.
- A configmap is a resource that can be used to store such non-confidential data in a k8s cluster inside etcd and can be mounted to pods, and can be used by applications directly!

![[Pasted image 20260328191910.png]]

### why is secret needed?

- The major difference between configmap and secrets is that, secrets usually contain confidential data which is stored in etcd but it is always encrypted by k8s before it is stored by k8s!
- 




## Links:

202603280927
