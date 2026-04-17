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


- store state file to a remote backend - it is always the best practice to store state files in a remote backend because it is easier to manager and more secure than storing locally
- never update or delete the state file as it might get corrupted and once the state file is lost, terraform cannot recollect the infra state
- state locking - the state file must be locked as when changes are made simultaneously by multiple users, it can cause conflicts! we must ensure a lock mechanism
- isolation of state file - maintain different state files for different environments
- regular backup - the state file must be regularly backed up which can be used for accidental deletion

### how to create the remote backend?



## Links:

202604162222
