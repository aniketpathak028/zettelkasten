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

### Containers vs VMs

- a container is a packaging of software code with just the operating system (OS) libraries and dependencies required to run the code to create a single lightweight executable
- more portable and resource-efficient than virtual machines (VMs)
- In simple words these can be consider tiny units of machine responsible for running an instance of application

![[containers vs vms.png]]

> the core difference in VM and Containers are containers virtualize the OS while VMs virtualize the hardware, hence containers are lightweight and faster to run!

| Feature              | Containers                   | Virtual Machines                    |
| -------------------- | ---------------------------- | ----------------------------------- |
| Virtualization Level | Operating System (OS) layer  | Hardware layer                      |
| Resource Usage       | Lightweight, fewer resources | Resource-intensive, higher overhead |
| Startup Time         | Fast (seconds)               | Slower (minutes)                    |
| Isolation            | Process-level isolation      | Full OS isolation                   |
| Kernel               | Shares the host OS kernel    | Each VM has its own kernel          |
| Portability          | Highly portable, move easily | Less portable, larger images        |
### What is Docker?

- an application for developing, shipping and running applications in containers, simplifies the process of container management!
- helps to containerize an application and containers could be as low as 50MB.
- simply put docker is a way of containerizing an application but is a better alternative than creating a VM!

> docker can be run by both docker desktop and rancher read [[rancher-desktop vs docker-desktop]]

### components of docker

- [[dockerfile]] - is a script containing a series of instructions and commands for building a docker image
- image - blueprint for creating containers
- container - a container that runs on the docker daemon

> [[dockerhub]] is a repository for storing docker images just like github stores codebases
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

[[containerization]]
[[docker]]

202509301423