---
title: helm
draft: false
tags:
  - helm
  - k8s
date: 2025-09-21
description: what the helm?
---
# what the [helm](https://helm.sh/)?

- helm is a package manager for kubernetes based applications
- helm runs as a binary on your local machine and when we run the helm command, it connects to the current kubernetes cluster using the config and performs actions similar to kubectl behind the scenes
- helm chart is a complete package for a kubernetes application containing all the resources needed to run the app, making lives of devs easier

### installing [homarr](https://homarr.dev/docs/getting-started/installation/helm/) using helm

```bash

# add a repo to local helm charts
helm repo add homarr-labs https://homarr-labs.github.io/charts/

# list all the helm charts
helm repo list

# update the helm charts
helm repo update

# install application using helm chart in a specific namespace (if not present create the namespace!)
helm install homarr homarr-labs/homarr --namespace homarr --create-namespace
```

> Homarr now needs a secret called "db-secret" without which it won't start!

create a db-secret for homarr

```bash
 k create secret generic db-secret --from-literal=db-encryption-keys='597171fe5103489b52ce71936728cc395267839b4d5d7b4b7b486d8ce31d295a' --namespace homarr
```


## Links:

202509211137