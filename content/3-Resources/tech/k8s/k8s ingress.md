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

### creating an ingress controller in rancher

we can simply create an ingress controller in rancher node using the following command
```shell
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.1.2/deploy/static/provider/cloud/deploy.yaml
```
once the nginx controller pod comes up and running we can create an ingress resource in our cluster!

> Note:
> the default ingress controller in rancher-desktop is traefik, and it must be first disabled in order to install and run nginx-controller!
> It can be disabled in rancher-desktop settings directly 

to check if the ingress controller pod is running or not use the command
```shell
kubectl get pods -A | grep nginx
```
if you see a pod names nginx-controller running than the nginx controller is successfully deployed in the cluster!

now lets learn more about ingress in detail deploying a simple flask application:



```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: minimal-ingress
spec:
  ingressClassName: nginx
  rules:
  - http:
      paths:
      - path: /testpath
        pathType: Prefix
        backend:
          service:
            name: python-django-app
            port:
              number: 80
```


## Links:

[[kubernetes]]
[[k8s storage]]

202509010120