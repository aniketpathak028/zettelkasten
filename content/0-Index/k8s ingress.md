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

Note: 
Ingress is the way to route URLs or FQDNs to ip addresses in a k8s cluster!

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

202509010120