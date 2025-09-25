---
title: sudo and apt-get
draft: false
tags:
  - sudo
  - apt-get
  - linux
date: 2025-09-24
description: sudo and apt-get
---
# sudo and apt-get

- apt-get update → update pkg manager

root → super user (has all the powers in the machine!)

> use sudo with any command to execute as a super user, provided you have access to super user (in ubuntu, the 1st user created has the sudo access!)

> to permanently execute commands as root user, it is better to login as root user or switch into root
### how to become the root user?

```bash
sudo su - # login as root user

# switch user
su "user name"
```

- sudo apt-get upgrade → update all the softwares on the system installed using apt-get
- apt-get install "name" → install a new software
- apt-get remove "name" → uninstall a software
- apt-cache search "name" → search in the local cache

> check out /etc/apt/sources.list

### difference between apt-get update and apt-get upgrade?

apt-get update → updates the list of available packages and their versions, but it does not install or upgrade any packages.

apt-get upgrade → actually installs newer versions of the packages you have. After updating the lists, the package manager knows about available updates for the software you have installed. This is why you first want to update.

### PPA - Personal Packaged Archives

- non standard software/updates
- generally used by people who want the latest and greatest

```bash
sudo add-apt-repository ppa:gwibber-daily/ppa
```

> As anybody can create a PPA there's no guarantee for quality or security of a PPA - just like with any other unofficial software source you have to decide yourself if a PPA it's trustworthy or not. And like any other unofficial software packages from a PPA can cause all sorts of difficulties especially when upgrading to a new release of Ubuntu.

> check out emacs
## Links:

[[sudo]]
[[linux]]

202509241716