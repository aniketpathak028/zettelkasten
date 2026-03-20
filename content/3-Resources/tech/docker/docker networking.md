---
title: docker networking
draft: false
tags:
  - docker
  - networking
date: 2026-03-20
description: how does docker networking work?
---
# Docker Networking

> best when read from here - https://docs.docker.com/engine/network/

Docker architecture has a simple networking structure where all the docker containers are connected to a single network called the bridge network by default also known as docker0 and using docker0 it can communicate with the host or other docker containers in the host. It can also communicate outside the host using the host network!

The issue with this is however that sometimes we might have critical applications in a container ex- payment related containers or containers containing any crucial data that should be allowed common access, in this situation the security of such a container is compromised so docker has customized networking options where users can create separate bridge networks for separate containers to create an isolation between containers.

![[docker networking.png|553]]







## Links:

202603200125
