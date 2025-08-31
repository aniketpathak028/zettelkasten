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
- containers in pods can communicate with each other through localhost

#### cni plugin
- container networking interface plugin
- provides n/w connectivity to containers
- configures network interfaces in containers
- assigns ip addresses and sets up routes -> iptables on nodes
- when we setup a cluster from scratch we often have to choose a cni plugin:
	- Cilium
	- Calico
	- Flannel





## Links:

202508311241