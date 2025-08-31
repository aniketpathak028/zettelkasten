---
title: namespaces
draft: false
tags:
  - namespaces
  - k8s
date: 2025-08-31
description: what are k8s namespaces?
---
# [namespaces](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

- logical grouping within a cluster to isolate resources
- names of resources need to unique within a namespace, but not across namespaces
- namespace-based scoping is applicable only for namespaced objects (ex- deployments, services, etc.)
- every app should have their own namespace!

```bash
k get namespaces # list all namespaces

k delete namespaces <namespace> # delete a ns

k run aniket --image=nginx -n mealie # create a pod in a specific namespace

k config set-context --current --namespace=mealie # set the default namespace for a context 

k config view | grep namespace # get the current namespace
```

namespace.yaml

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: mealie
```


## Links:

202508302353