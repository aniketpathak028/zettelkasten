---
title: k8s networking
draft: false
tags:
  - k8s
  - networking
date: 2025-08-31
description: how k8s manages its networking?
---
# networking

### things to know:
#### pods
- k8s handles networking at pod level (so k8s doesn't connect containers but pods to each other)
- each pod gets its own ip address on the cluster, run `k get pods --all-namespaces -o wide`, k8s has a pool of IPs from which it allocated IPs!
- by default pods can connect to all pods on all nodes, but there are ways of limiting this using the networking policies which can get very granular
- containers in pods can communicate with each other through localhost, as a pod can have multiple containers running at the same time!

#### cni plugin - the tool to help k8s do all the n/w ing
- container networking interface plugin
- provides n/w connectivity to containers in the cluster
- configures network interfaces in containers
- assigns ip addresses and sets up routes -> iptables on nodes
- when we setup a cluster from scratch we often have to choose a cni plugin:
	- Cilium
	- Calico
	- Flannel - rancher desktop uses this as its CNI plugin!

Note:
to checkout we can use the `rdctl shell` command to enter into the rancher desktop VM that runs the cluster and we can navigate to /etc/cni to checkout the CNI plugin.


checkout [[k8s services]]

## Links:

[[k8s services]]

202508311241