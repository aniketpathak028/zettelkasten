---
title: docker-commands
draft: false
tags:
  - docker
  - containerization
  - VM
date: 2025-08-10
---
commands I keep forgetting 😅

```

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

high time I start remembering them!

~aniket

