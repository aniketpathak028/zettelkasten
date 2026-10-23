---
title: container runtimes
draft: false
tags:
  - docker
  - buildah
  - containers
  - container-runtime
date: 2026-03-18
description: docker vs podman vs buildah vs cri-o
---
# Docker vs Buildah

Docker is a perfect tool but there is one problem, docker relies heavily on Docker engine which is a docker daemon that runs in the background! What if this engine fails, all our containers would be stopped?

Buildah to rescue - https://minimaldevops.com/buildah-and-docker-are-both-tools-for-building-container-images-but-they-have-some-key-differences-a3530b923be0

There are also many other container runtime like Podman, ContainerD, CRI-O

![[different container runtimes.png]]


## Links:

[[docker]]
[[containerd]]

202603181638
