---
title: RBAC
draft: false
tags:
  - RBAC
date: 2026-03-29
description: what is RBAC?
---
# RBAC - Role Based Access Control

> Note - read https://kubernetes.io/docs/reference/access-authn-authz/rbac/

RBAC has 2 parts 
- Users management - ie. who can access which resources in the cluster!
- Service Accounts management - ie. which services can access what in the cluster!

How is it done?
- service account / users - it is the user identification that helps k8s understand user's privileges.
- roles / cluster role - these are k8s resources that can be attached to any user at pod level or cluster level using role-binding!
- role binding / crb - these are k8s api to bind a role to a service account!

How K8s handles user management?
- K8s offloads the user management to 3rd party Identity providers like AWS - IAM, Azure, or GCP, Keyclook etc!

 






## Links:

202603291104
