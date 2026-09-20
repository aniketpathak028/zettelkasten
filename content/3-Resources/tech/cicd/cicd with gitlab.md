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
- step-2: create a VM in any cloud platform, here I create an EC2 instance on AWS and create a security group with the following inbound rules, and attach this group to my instance:
![[Pasted image 20260920001548.png]]

### how to use a runner?
- go to the repository settings -> ci/cd -> runners -> create project runner
- connect to your ec2 instance on AWS using ssh
- install gitlab-runner in the vm and register it with gitlab using the code snippet in gitlab
- once it shows green symbol, the runner is registered!

```bash
chmod 400 secret.pem
ssh -i secret.pem ubuntu@<ip-address>
sudo apt update

# now install the gitlab-runner to this vm using the commands from gitlab
# register it with the gitlab runner using the code snippet
gitlab-runner run
```
















## Links:

202609191631
