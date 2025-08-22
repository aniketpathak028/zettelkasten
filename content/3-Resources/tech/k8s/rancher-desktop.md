---
title: rancher-desktop
draft: false
tags:
  - k8s
date: 2025-08-21
---
# rancher desktop

- open-source app
- provides container mgmt + k8s on local machine
- allows devs to build, push, and pull container images
- run container using containerd or dockerd(moby)
- uses k3s 

Note:
`There is a .kube folder in home containing a config file which rancher configures in order for us to access pods smoothly!`


in short:
rancher desktop is helping you in 2 ways:
- lets u setup and run a k8s cluster on your local machine inside a VM!
- provides you a container runtime with (nerdctl or dockerd) to help you run containers (pull, push and run images on containers)

miscenalleous stuff:
- to know about ur current k8s context check
```
kubectl config current-context
```
- if you're runnning k8s cluster with rancher it should print out rancher-desktop, if not check .kube/config for k8s config
```
apiVersion: v1
kind: Config
clusters:
  - name: rancher-desktop
    cluster:
      server: https://127.0.0.1:6443
      certificate-authority-data: LS0tLS1CRUdJTiBDRVJUS
      insecure-skip-tls-verify: false
users:
  - name: rancher-desktop
    user:
      client-certificate-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FU
      client-key-data: LS0tLS1CRUdJTiBFQyBQUklWQVRFIEt
contexts:
  - name: rancher-desktop
    context:
      cluster: rancher-desktop
      name: rancher-desktop
      user: rancher-desktop
preferences: {}
current-context: rancher-desktop

```

## Links:

[[kubernetes]]

202508212225