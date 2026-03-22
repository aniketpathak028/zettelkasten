---
title: Untitled
draft: false
tags:
date:
description:
---
# K8s architecture

### What are the major differences between K8s and docker?

- Docker uses a container-runtime to containerize applications known as [[containerd]] however K8s allows us to use any container runtime which implements K8s [[container runtime]] interface -  cri-o, containerd etc

>Note: more about runtimes https://docs.docker.com/engine/daemon/alternative-runtimes/

- In docker, the docker daemon or docker engine is responsible for creating, running and deleting the containers (smallest unit of docker) while in K8s it is kubelet which is responsible to always keep a pod running (smallest unit of k8s)!
- In docker, the networking of containers is taken care by the default bridge network - docker0, in k8s kube-proxy takes care of all the networking related stuff like - assigning ip to pods, creating a load-balancer, etc.
- 







## Links:

202603220953
