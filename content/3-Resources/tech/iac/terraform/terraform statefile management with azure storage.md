---
title: tf statefile management with az-storage
draft: false
tags:
  - terraform
  - terraform-statefile
  - azure-storage
date: 2026-04-16
description: what is tf statefile and how it should be managed?
---
# terraform statefile

![[Pasted image 20260416222528.png]]

### how does terraform know what changes to make?

- it stores the current state of the infra in a file called the `terraform.tfstate`
- this file contains all the metadata about the resources in the infra
- tf uses this file to directly compare what changes it must do to make `current state = desired state` 

> Note: when we run terraform plan it creates this file and stores in our PC! it is not the best thing to do, and it is always better to store it in a remote backend!
### state file best practices

![[Pasted image 20260417104751.png]]




## Links:

202604162222
