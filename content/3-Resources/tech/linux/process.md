---
title: process
draft: false
tags:
  - process
  - linux
date: 2025-09-24
description: what is a process in linux kernel?
---
# what is a process?

anything that the kernel spawns to do some work is a process starting from opening a browser to a simple command to list files in a directory!

> process → kernel → hardware

```bash
ps -ef # shows all the running processes with detailed info
```
### parts of a process:

- address space → physical address (RAM) virtual address
- kernel data-structures → info (who owns the process?, address space, priority….. etc)

### each process has:

- PID → an id called process id
- UID → which User owns the process!
- Effective UID → give process the permissions which are effective to the process and not the same powers as the process that spawned it!
- Niceness → how nice is it? low priority ↔ higher niceness!

> run the command htop! or ps aux to list all the processes running on the system

> “init” is the mother of all processes (which has PID 1) however containerized VMs could be an exception! init is the first process that the kernel spawns on boot, and it is responsible for launching other processes and startup scripts! Incase a parent process is killed at any moment, it’s children processes are allocated to init!

### concept of parent and child process

- When a process is started, it is spawned by the kernel and when the parent process needs to spawn a child process, it creates a copy of itself called a fork, and this forked process is what spawns a child process, once the child process is done with its work, it notifies the kernel and the kernel kills it, and provides the return value of the child process to the parent!
- different OS have different init systems

> read about the different init systems
> - systemd
> - sysv init
> - upstart
> - openRC
> - runit


## Links:

[[linux]]
[[process]]
[[process signals]]

202509241815