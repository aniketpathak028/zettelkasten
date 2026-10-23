---
title: dockerhub
draft: false
tags:
  - docker
  - dockerhub
  - docker-images
date: 2025-10-02
description: what is dockerhub?
---
# What is dockerhub?

dockerhub is a central repository for storing docker images both by organizations and by individuals for community and personal use!

> its like github but for containers! you can also make them private or public!
> 
> there are container registries for cloud providers too like azure, gcp, aws and github etc.
### how to publish an image in dockerhub?

step-1: create a dockerhub account and authenticate with cli

step-2: create a new repository

step-3: copy the command to push the local image to dockerhub

step-4: tag the local image. read https://docs.docker.com/reference/cli/docker/image/tag/
```bash
docker tag docker-fastapi:latest aniketpathak028/docker-fastapi:latest
```

`docker image tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]`

step-5: push the local image to dockerhub
```bash
docker push aniketpath028/docker-fastapi:latest
```

## Links:

[[docker]]

202510020100