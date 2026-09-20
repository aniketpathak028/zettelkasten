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

### create a pipeline
- once the runner is set up, go to gitlab project > build > pipeline editor and create a new pipeline
- in the pipeline we will define stages and jobs that will be automatically triggered when we push code changes to gitlab
- a simple pipeline to install necessary dependencies and tools in the VM and run unit tests:
```yml
stages: # List of stages for jobs, and their order of execution
- install_tools
- test

install_mvn_trivy_docker_kubectl:
stage: install_tools
script:
- sudo apt install openjdk-17-jre-headless -y
- sudo apt install maven -y
- sudo apt-get install wget gnupg -y
- wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
- echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb generic main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
- sudo apt-get update && sudo apt-get install trivy -y
- sudo apt install docker.io -y && sudo chmod 666 /var/run/docker.sock
- sudo snap install kubectl --classic

tags:
- runner-ec2

unit_testing:
stage: test
script:
- mvn test

tags:
- runner-ec2
```
- once the basic pipeline works we need to install sonarqube in our vm using docker and start the sonarqube server and access it using {ipaddress}:9000
- by default the username and password is admin
```bash
docker run -d -p 9000:9000 sonarqube:lts-community 
```












## Links:

202609191631
