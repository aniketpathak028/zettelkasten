---
title: k8s ingress
draft: false
tags:
  - k8s
  - ingress
date: 2025-09-06
description: how does k8s ingress work?
---
# ingress

> Note: 
    Ingress is the way to route URLs or FQDNs to ip addresses in a k8s cluster!

### why is ingress needed? - problems with k8s service
- k8s service does not offer enterprise & TLS based load balancing capabilities like:-
	- sticky sessions
	- TLS
	- path based
	- host based
	- ratio based etc.
- for every load balancer created in k8s, the cloud provider creates a static public IP which is expensive!
### solution
- K8s came up with a solution that since they cannot write the logic for all the different kind of loadbalancers like nginx, haproxy, f5 etc. it asked them to write an ingress controller for k8s which can be implemented by the customer as per his choice of load balancer.
- so now the user just needs to decide which loadbalancer he wants to choose for his application and first create an ingress controller for the same and then simply create an ingress resource with an ingress rule for all his services!
### things to know
- ingress is a resource on the cluster
- exposes http and https routes from outside the cluster to services within the cluster
- provides SSL and TLS termination
- helps route external URLs or FQDNs
- path based routing is allowed too!
- Ingress resource is implemented by Ingress Controller similar to any other k8s resource like pods, svc, depl, namespace etc.
- Ingress controller - nginx, traefik, cilium, cloud: agic

![[k8s-ingress-architecture.png]]
## Links:

[[kubernetes]]
[[k8s storage]]

202509010120