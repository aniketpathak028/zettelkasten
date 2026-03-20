---
title: multi-stage builds in docker
draft: false
tags:
  - docker
  - multi-stage-build
date: 2026-03-20
description: practical problems with docker
---
# Multi-stage builds

> Best when read from here -> https://docs.docker.com/build/building/multi-stage/

Concept:
- A general dockerfile contains a base image usually an OS base image like ubuntu, centos etc
- on top of this base image we transfer our codebase and install our dependencies for the application and finally run it once we have all the requirements!
- But the final goal is to always just run the application hence there is technically no need for having a base os and the app code, we could simply use the app build and a minimalistic runtime with no dependencies and code!

This is the concept of Multi-stage docker builds :)

### Advantage of dockerfile with multi-stage builds

Let's say we have a simple dockerfile without any multistage builds that containerizes a simple Go application, let's build this docker image and check its size!

```dockerfile
FROM ubuntu AS build

RUN apt-get update && apt-get install -y golang-go

ENV GO111MODULE=off

COPY ..

RUN CGO_ENABLE=0 go build -o /app .

ENTRYPOINT [/app]
```

It's almost 1GB, let's now see if we can reduce this using multistage dockerfile!

```dockerfile
FROM ubuntu AS build

RUN apt-get update && apt-get install -y golang-go

ENV GO111MODULE=off

COPY ..

RUN CGO_ENABLE=0 go build -o /app .

FROM scratch

COPY --from=build /app /app

ENTRYPOINT [/app]
```

Can you guess the size now? it's only 3.19 MB! From 1GB -> 3.19MB it's crazy good :)

### Advantages

So there are overall 2 advantages of this kind of build:
- It reduces the size of the docker images making them very lightweight, minimalistic and definitely faster!
- It also reduces security vulnerabilities because the final image is usually distroless or very minimal not allowing much operations possible in the container incase it is hacked!

these distroless images for all usecases can be found here - https://github.com/googlecontainertools/distroless

## Links:

202603200014
