---
title: cicd with gitlab
draft: false
tags:
  - ci-cd
  - gitlab
date: 2026-09-19
description: deploying a java spring boot microservice using gitlab cicd pipeline
---
# CICD pipeline on gitlab

### why gitlab is better?

- for jenkins we need to setup master and slave nodes which need 2 VMs
- we also need to store our codebase in github or gitlab and then connect it to jenkins
- gitlab cicd is better because we can directly store and deploy our code using gitlab
- gitlab provides shared runner and private runner
- shared runner - this is free provided by gitlab but we cannot access the VM
- private runner - this should be created by us (ex- VMs, k8s pod etc) 

![[Pasted image 20260919232831.png]]

- step-1: create the repository in gitlab with the project for this example we use - https://gitlab.com/aniketpathak/Boardgame
- step-2: create a VM in a cloud platform or somewhere else here I create an EC2 instance on AWS and create a security group with the following inbound rules:
![[Pasted image 20260920001548.png]]

















## Links:

202609191631
