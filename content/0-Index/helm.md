---
title: helm
draft: false
tags:
  - helm
  - k8s
date: 2025-09-21
description: what the helm?
---
# what the helm?

- helm is a package manager for kubernetes based applications
- helm runs as a binary on your local machine and when we run the helm command, it connects to the current kubernetes cluster using the config and performs actions similar to kubectl
- read https://helm.sh/

### installing [homarr](https://homarr.dev/docs/getting-started/installation/helm/) using helm

```bash

# add a repo to local helm charts
helm repo add homarr-labs https://homarr-labs.github.io/charts/

# list all the helm charts
helm repo list

# update the helm charts
helm repo update

# install application using helm chart in a specific namespace (if not present create the namespace!)
helm install homarr homarr-labs/homarr --namespace homearr --create-namespace

```






## Links:

202509211137