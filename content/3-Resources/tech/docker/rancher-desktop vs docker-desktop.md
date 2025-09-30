---
title: rancher-desktop vs docker-desktop
draft: false
tags:
  - docker-desktop
  - rancher-desktop
  - containerization
date: 2025-08-31
description: what is the difference between rancher and docker desktop?
---
# rancher-desktop vs docker-desktop
### things to know:

- rancher-desktop uses [[containerd]] as its container runtime by default, even docker-desktop uses containerd!
- however, it provides a compatible docker api meaning we can use the standard docker cli to interact with rancher's container management
- to use docker cli set container engine as dockerd (moby) in settings
- the point to note is DOCKER_HOST env should point to Rancher's docker socket.

```bash
docker context ls # list contexts and the current one
docker context use rancher-desktop # switch context to rancher desktop
```

- if docker desktop is installed on the system, it might be claiming the docker socket which rancher might want to use, this can lead to problems where the docker commands are directed to docker desktop instead of rancher desktop, so make sure to be in the correct context!

#### difference
- both use containerd as container runtime engine but rancher does not run the full docker engine, instead it provides a docker compatible api layer through [[cli-nerdctl]]
- docker-desktop includes its own distribution of k8s, but rancher lets us use multiple distributions - k3s and also lets us configure and manage diff k8s versions
- docker-desktop has commercial license however rancher is fully open-source
- rancher with k3s is much more lightweight than docker-desktop



## Links:

[[kubernetes]]

202508311811