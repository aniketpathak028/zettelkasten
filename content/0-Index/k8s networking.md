---
title: k8s networking
draft: false
tags:
  - k8s
  - networking
date: 2025-08-31
description: how k8s manages its networking?
---
# k8s networking

### things to know:
#### pods
- k8s handles networking at pod level (so k8s doesn't connect containers but pods to each other)
- each pod gets its own ip address on the cluster, run `k get pods --all-namespaces -o wide`, k8s has a pool of IPs from which it allocated IPs!
- by default pods can connect to all pods on all nodes, but there are ways of limiting this using the networking policies which can get very granular
- containers in pods can communicate with each other through localhost, as a pod can have multiple containers running at the same time!

#### cni plugin - the tool to help k8s do all n/w ing
- container networking interface plugin
- provides n/w connectivity to containers in the cluster
- configures network interfaces in containers
- assigns ip addresses and sets up routes -> iptables on nodes
- when we setup a cluster from scratch we often have to choose a cni plugin:
	- Cilium
	- Calico
	- Flannel - rancher desktop uses this as its CNI plugin!

Note:
to checkout we can use the `rdctl shell` command to enter into the rancher desktop VM that runs the cluster and we can navigate to /etc/cni to checkout the CNI plugin

### services

- think of services are grouping of pods! ex- frontend svc, backend svc
- we can define a frontend svc for ex and k8s figures out the pod level stuff like ip address, scaling up and down the pods based on metrics etc.

#### why do we need services?
- pods are ephemeral, we should not expect a pods to have a long lifespan.
- Pods are constantly changing and being moved across nodes.
- How will the system keep track of the constantly changing IP addresses?


## Links:

202508311241