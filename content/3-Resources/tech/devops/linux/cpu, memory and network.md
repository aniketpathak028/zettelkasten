---
title: cpu, memory and network
draft: false
tags:
  - cpu
  - memory
  - linux
  - linux-commands
date: 2025-09-25
description: cpu, mem and network commands
---
# cpu, memory and network commands

- df -h-> disk space usage in human readable format (mb, kb, gb)
- free -g-> mem usage (ram and swap memory) in gigabytes
- top -> mem, cpu and disk together
- nproc-> shows the number of available CPU cores in the system
- htop (just an advanced version of top)
    - default tool that lists all the processes and threads running/sleeping on the system
    - displays the system load, cpu usage and other sys stats
    - lists all the processes with PIDs, Command., cpu usage, port etc.
- netstat
	- default tool to view n/w connections, ports, and routing table in the machine
```bash
netstat -a # shows all tcp and udp connections
netstat -lntu # l -> listening, -n -> ip/port, -t -> tcpm, -u -> udp
```


> read more about these commands!

## Links:

202509250909