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
## Why to script?
- scripting is a part of automation, which is essential to reduce the manual effort needed to do repetitive tasks!
- shell scripts can help reduce such manual efforts on linux servers by automating them.

## How to write a script?

- shebang -> #!
- exec path -> /bin/bash (executable shells : ksh, sh, dash, aix, bash etc)
- bash is the most commonly used shell for scripting however any of the shell can be used!
- in some bash scripts, the path might be /bin/sh as it is a symlink to bash (/bin/sh -> /bin/bash)
- however recently, ubuntu has started linking /bin/sh -> /bin/dash

```shell
#!/bin/bash

# print
echo "hello world!"
```







## Links:

202509222244