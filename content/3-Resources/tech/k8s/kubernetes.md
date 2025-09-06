---
title: kubernetes
draft: false
tags:
  - k8s
  - container-orchaestration
date: 2025-08-21
description: the most amazing piece of tech every dev should know!
---
# [Kubernetes](https://kubernetes.io/)

`Note: the k8s docs are your bible to learn anything about k8s!

rule of thumb 👍:
`to learn about any command always use the cli with --help subcommand if it is present (most linux cli tools have it!) only if it doesn't explain very well go to the docs 🙂`

## what is k8s (my POV)?
- after [[containerization]] came into picture, people started containerizing apps inside VMs, and to scale it multiple VM copies were created.
- Bottleneck?
	- what if I need to create several 100 of these replicas?
		- lot of manual work ([[ansible]] playbook)
		- manual deletion and scaling of VMs
		- if containers crash it had to be respawned manually
		- a container was unaware about its own replicas in other VMs
- enter k8s! (the savior 🦸)
	- a container orchestration tool
	- an OS for the VMs (now the cloud)
	- manages the VMs using control plane (which is a VM in itself), the VMs are called worker nodes (they can also be physical machines)
	- the control plane takes the desired state of the containers from the user and achieves it through its worker nodes
- benefits ➕
	- no manual work
	- just state your desired state of containers in a YAML file and k8s achieves it!
	- k8s also has the ability to automatically scale up or down based on metrics like cpu usage, number of requests, mem usage, time of the day, or any other metric! - no manual scaling
	- if a container crashes, it respawns another one, takes care of all the networking and traffic (basically it maintains the desired state of the application without hampering business) - amazing piece of tech right? 😍

A wonderful picture to explain how k8s works in a local setup using rancher desktop:

- [[kubectl]] - a terminal tool to manage the k8s cluster
- [[control plane]] - manages the worker nodes and takes instructions from api server which exposes k8s apis, it also has a scheduler to schedule pods and ETCD to preserve the state of the app so that no data gets lost!

![[k8s-architecture.png]]
in a typical prod setup, a k8s cluster consists of few worker nodes (or VMs) handling the workload and a control plane node to which the [[kubectl]] commands interact to declare the desired state of the app!
## Links:

[[kubectl]]
[[rancher-desktop]]
[[pod]]
[[deployment]]
[[k8s networking]]

202508202239