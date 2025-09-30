---
title: what is docker?
draft: false
tags:
  - docker
  - containerization
date: 2025-09-30
description: learn the fundamentals of docker
---
# What is Docker?

### What is Containerization?

- packaging of software code with just the operating system (OS) libraries and dependencies required to run the code to create a single lightweight executable—called a container
- portable and resource-efficient than virtual machines (VMs).
- In simple words these can be consider tiny units of machine responsible for running an instance of application!

### What is Docker?

- a program that performs operating-system-level virtualization, also known as "containerization". 
- helps to containerize an application and containers could be as low as 50MB.
- simply put docker is a way of containerizing an application but is a better alternative than creating a VM!

![[containers vs vms.png]]

> the core difference in VM and Containers are containers virtualize the OS while VMs virtualize the hardware, hence containers are lightweight and faster to run!

> docker can be run by both docker desktop and rancher read [[rancher-desktop vs docker-desktop]]


### commands

```shell
docker ps # list running containers

docker ps -a # list all containers

docker images # list all images

docker pull {image}:tag # pull an image with a specific tag

docker run {image}:tag # run a container using an image
# if the image is not present it fetches it first

docker run -d {image}:tag # run in detached mode - no logs

docker logs {container-id} # print logs

docker run -d -p 8080:80 nginx 
# forwards container port 8080 -> port 80 of localhost

docker build -t {name}:tag .
# build the docker image from the dockerfile in pwd

docker exec -it <container_id or name> /bin/bash
# enter docker container
```


## Links:

202509301423