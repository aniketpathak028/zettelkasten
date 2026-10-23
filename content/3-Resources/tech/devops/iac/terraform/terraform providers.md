---
title: terraform providers
draft: false
tags:
  - terraform
  - azure
date: 2026-04-14
description: terraform providers
---
# terraform provider - azure tf

notes- https://github.com/piyushsachdeva/Terraform-Full-Course-Azure/tree/main/lessons/day02

## Why do you need a Terraform provider?

A Terraform provider is a plugin that acts as a translator between Terraform and external APIs, enabling the management of cloud services, SaaS, and infrastructure. It translates HashiCorp Configuration Language (HCL) into API calls, allowing for the creation and management of resources like virtual machines, databases, or networking components

### provider version vs terraform core version

- provider version must be supported by the core version else the code won't work!
- as by default the core version is the latest version but it may not support certain resources in provider version
- hence, it is important to make sure the config is compatible with the core version


## Links:

202604141142
