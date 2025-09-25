---
title: how to write a shell script?
draft: false
tags:
  - shell
  - scripting
  - automation
  - linux
date: 2025-09-22
description: how to write a shell script?
---
# why to write a shell script?

- scripting is a part of automation, which is essential to reduce the manual effort needed to do repetitive tasks!
- shell scripts can help reduce such manual efforts on linux based kernels by automating them using bash or any other shell commands.
- other programming languages like Go and Python may also be used but shell (bash, ksh, zsh, or fsh) is the most unix native language to talk to the kernel, hence it is often more reliable, faster, and more compatible for scripting.
- and ofcourse it is cool AF! 😎

### how to write a script?

- every shell script has this line at the very beginning "#!/bin/bash" which indicated what kind of shell script it is and the path of the shell executable!
	- shebang -> #!
	- exec path -> /bin/bash (executable shells : ksh, sh, dash, aix, bash etc)
- bash is the most commonly used shell for scripting however any other shell can be used too!
- in some bash scripts, the path might be /bin/sh as it is a symlink to bash (/bin/sh -> /bin/bash)
- however recently, ubuntu has started linking /bin/sh -> /bin/dash, so it is imp to clearly specify the type of the shell.

### a simple script to print the system health info

```bash
#!/bin/bash

#####################
# Author: Aniket
# Date: 23 Sept 2025
# This script outputs node health
# Version: v1
#####################

# to print the command everytime before executing
set -x          # debug mode
set -e          # exit the script when there is an error
set -o pipefail # exits the script when there is a pipefail

df -h

free -g

nproc

ps -ef | grep "sysmond" | awk -F' ' '{print $1}'
```



## Links:

[[shell]]
[[linux]]

202509222244