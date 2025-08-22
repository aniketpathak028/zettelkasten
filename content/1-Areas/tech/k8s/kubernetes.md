---
title: kubernetes
draft: false
tags:
  - k8s
  - container-orchaestration
date: 2025-08-21
---
# [Kubernetes](https://kubernetes.io/)

`the k8s docs are your bible to learn anything about k8s`

what is k8s?
- after containerization came into picture, people started containerizing apps inside VMs and to scale it, multiple VM copies were created.
- Bottleneck?
	- what if I need to create several 100 of these replicas?
		- lot of manual work (ansible playbook)
		- manual deletion and scaling of VMs
		- if containers crash it had to be respawned manually
		- a container was unaware about its own replicas in other VMs
- enter k8s!
	- a container orchaestration system
	- sort of an OS for the cloud/VMs
	- manages the VMs using control plane (which is a VM in itself), the VMs are called worker nodes (they can also be physical machines)
	- the control plane takes the desired state of the containers from the user and achieves it through its worker nodes
- benefits
	- no manual work
	- just state your desired state of containers in a YAML file and k8s achieves it!
	- k8s also has the ability to automatically scale up or down based on metrics like cpu usage, number of requests, mem usage, time of the day, or any other metric! - no manual scaling
	- if a container crashes, it respawns another one, takes care of all the networking and traffic (basically it maintains the desired state of the application without hampering business) - amazing piece of tech 😍

![[k8s.png]]


## Links:



202508202239