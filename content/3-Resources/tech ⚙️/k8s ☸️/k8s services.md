---
title: k8s services
draft: false
tags:
  - k8s
  - service
  - deployment
date: 2025-08-31
description: what are k8s services?
---
# Services

- think of services are grouping of pods! ex- frontend svc, backend svc
- we can define a frontend svc and the svc figures out the pod level stuff like ip address, scaling up and down the pods based on metrics etc.
![[k8s-services.png]]
#### depl vs svc

Kubernetes service enables network access to a set of Pods while **Kubernetes deployment is in charge of keeping a set of pods running**. Kubernetes services and deployments can't be compared as they perform different functions, but they complement each other nicely. When a deployment is exposed it becomes a service!

#### why do we need services?

- pods are ephemeral, we should not expect a pod to have a long lifespan.
- pods are constantly changing and being moved across nodes.
- how will the system keep track of the constantly changing IP addresses?

```bash

# expose a deployment and generate a svc - not used in prod
kubectl expose deployment frontend --port 8080

# fetch services
kubectl get svc

# forward the service port
kubectl forward svc/mealie 9000
```

- a service has a cluster ip and a name that can be used for internal dns resolution in k8s!

### Types of Services
- ClusterIp - default, creates a cluster wide ip for the service.
- NodePort - exposes a port on each node allowing direct access to the service through any node's ip address, try avoiding this approach.
- LoadBalancer - mostly used for cloud providers, creates an Azure LoadBalancer to route traffic into the cluster. (can also be used in k3s/Rancher desktop)

```bash
# generate yaml for service
kubectl get svc mealie -o yaml > service.yaml

# delete a service
kubectl delete svc/mealie
```

```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: mealie
  name: mealie
  namespace: mealie
spec:
  ports:
  - port: 9000
    protocol: TCP
    targetPort: 9000
  selector:
    app: mealie
  type: LoadBalancer
```
## Links:

[[k8s networking]]
[[k8s ingress]]

202508312348