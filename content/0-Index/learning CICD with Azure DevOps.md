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

![[architecture example voting.png|357]]

Fork the repo and clone it locally and run `docker compose up` to test the app locally!
Now that we have a rough idea of the architecture, we can get started!

### Step-1: Azure DevOps and Azure account

Make sure you have an Azure DevOps (https://dev.azure.com) and a Microsoft Azure (https://portal.azure.com) account! Both are different and it is always better to have a single microsoft account on both!

### Step-2: Creating Azure DevOps project and setting up the repo

- Create a new project in Azure DevOps

![[azure-project-creation.png|697]]

- import the repository to Azure DevOps from GitHub using HTTPS or SSH

> Note: Incase the main branch is not selected by default for the project go to branches and set the main branch as the default!

![[import repo azure.png|697]]

### Step-3: Creating container registry in Azure portal

Before we start building our pipelines for the microservices which pushes the docker images into the Azure container registry, let's create the registry first in Azure portal


























## Links:

202603131831
