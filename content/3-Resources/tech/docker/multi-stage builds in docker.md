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






## Links:

202603200014
