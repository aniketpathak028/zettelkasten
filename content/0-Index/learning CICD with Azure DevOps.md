---
title: Learning CICD with Azure DevOps
draft: false
tags:
  - azure
  - ci-cd
  - devops
  - k8s
  - docker
  - microservices
date: 2026-03-13
description: learn how to build your own Azure DevOps pipeline with continuous integration and continuous deployment
---
# Azure CICD

In this blog, we are going to learn how to build an Azure CICD pipeline using Azure DevOps by implementing it for a real time voting app - [[https://github.com/dockersamples/example-voting-app]], this is a sample microservices app built by the docker team which implements the principles of distributed systems mimicking a real life scenario. We will deploy this app into Azure Devops and create CI-CD pipelines for the microservices. Let's get started!

### Architecture - Voting app

The github repo has a comprehensive architecture explanation but in short there are 3 microservices in this application:
- a voting microservice written in Python that let's users vote
- a worker microservice that writes the in memory data from redis DB to a persistent Postgress DB written in .NET
- a result microservice written in Node.js that displays the live results of the poll
https://raw.githubusercontent.com/dockersamples/example-voting-app/main/architecture.excalidraw.png







## Links:

202603131831
