---
title: docker storage - bind mounts and volumes
draft: false
tags:
  - docker
  - docker-volumes
  - docker-bind-mounts
date: 2026-03-20
description: what are docker bind mounts and volumes?
---
# docker storage

> for the best wisdom - https://docs.docker.com/engine/storage/
> beautifully written docs by docker team!

docker storage - volumes, bind mounts 
### what was the challenge?

- docker containers are ephemeral, which means the data in the containers get destroyed when the containers get destroyed!
- so if you are running an application that stores some critical data, you might lose it if the container stops running due to any reason, this is a very big issue.
- To solve this docker provides persistent storage for containers using 3 storage mount options - volume mounts, bind mounts, tmpfs mounts and named pipes!
- no matter which mount you choose the data looks the same from inside the container!

### difference between volume & bind mounts

- bind mounts are a way using which you can bind a local container directory to a host directory running the container such that any change in either reflects in the other. 
- a volume on the other hand could be anything for ex an ec2 instance, a folder in the host fileserver, or any cloud storage outside the host!
- a volume is much more flexible than bind mounts as:
	- volumes are easier to backup and scale than bind mounts
	- volumes can be managed using docker-cli or docker-api directly
	- a volume can be shared by multiple containers
	- a volume can be used for high performance I/O

> always go with a volume storage over bind mount unless you have a specific usecase where bind mount is better!

###  docker volume commands

```shell
# create a docker volume
docker volume create <volume-name>

# list all volumes
docker volume ls

# delete a docker volume
docker volume rm <volume-name>

# to inspect a volume 
docker volume inspect <volume-name>

# mount a volume to docker container
docker run -d --name container --mount type=volume,src=aniket,dst=/app nginx:latest

```



## Links:

202603201228
