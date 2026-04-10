---
title: docker compose
draft: false
tags:
  - docker-compose
date: 2026-04-09
description: what is docker-compose and why is it needed?
---
# docker compose

> best when read from here - https://docs.docker.com/compose/

docker compose is useful when we want to run and manage multiple containers in a single host using a single command!

![[Pasted image 20260409185200.png|488]]

### difference in running containers using plain docker vs docker-compose!

Let's take the classic voting app example by docker - 
#### only docker
```shell
docker run -d --name=redis redis # run the redis container

docker run -d --name=db postgres # run the postgres container

docker run -d --name=vote -p 5000:80 voting-app # run the voting-app image and fwd the container port 80 to host port 5000

docker run -d --name=result -p 5001:80 result-app # run the result-app image and fwd the container port 80 to host port 5001

docker run -d --name=worker worker # run the worker microservice
```



## Links:

202604091736
