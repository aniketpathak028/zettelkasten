---
title: What are containers?
draft: false
tags:
  - containers
  - docker
date: 2026-03-18
description: What is the difference between Virtual Machines and Containers?
---
# Containers

- The major difference between Containers and Virtual Machines are Containers run on a single host operating system and doesn't have its own full Operating System unlike Virtual Machines!
- Containers have a small mini OS which contains the application code, application libraries and the system requirements to run the app!
- So, technically many Containers running on the same VM are not logically isloated from one another and can still talk to each other directly or through the host OS! But VMs are completely isolated as the hypervisors let them have their own independent Operating Systems!

![[container vs VM.png]]

### Containers vs VMs

- a container is a packaging of software code with just the operating system (OS) libraries and dependencies required to run the code to create a single lightweight executable
- more portable and resource-efficient than virtual machines (VMs)
- In simple words these can be consider tiny units of machine responsible for running an instance of application

> the core difference in VM and Containers are containers virtualize the OS while VMs virtualize the hardware, hence containers are lightweight and faster to run!

| Feature              | Containers                   | Virtual Machines                    |
| -------------------- | ---------------------------- | ----------------------------------- |
| Virtualization Level | Operating System (OS) layer  | Hardware layer                      |
| Resource Usage       | Lightweight, fewer resources | Resource-intensive, higher overhead |
| Startup Time         | Fast (seconds)               | Slower (minutes)                    |
| Isolation            | Process-level isolation      | Full OS isolation                   |
| Kernel               | Shares the host OS kernel    | Each VM has its own kernel          |
| Portability          | Highly portable, move easily | Less portable, larger images        |

## Links:

[[docker]]
[[container]]

202603181502
