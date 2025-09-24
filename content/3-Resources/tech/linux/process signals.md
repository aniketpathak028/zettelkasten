---
title: process signals
draft: false
tags:
  - process
  - signals
  - linux
date: 2025-09-24
description: process signals
---
# process signals

signals are how processes communicate to each other or to/from the kernel about the state of the system!

for ex - if a process wants to read from disk, the kernel will give it a signal once the disk is ready to be read by it!

> read https://man7.org/linux/man-pages/man7/signal.7.html

> consider signal as an interrupt to notify a process that some event has occurred!

### what can a signal do?

a signal can tell a process to:
- stop
- pause
- continue
- terminate
- reload config
- handle exceptional events (like seg faults)

### how signals work?

- every process has a PID
- signals are send to PID using commands or internally
- the process receiving signal can:
	- handle it (is it has a signal handler defined in its code)
	- ignore it (for some signals)
	- use the default action (kill, stop, etc.)

### sending signals

the most common way to send signal is the kill command

```bash
kill -SIGTERM 1234 # sends the SIGTERM signal to process with id 1234

or

kill -15 1234 # each signal has a number 15 = SIGTERM
```

| Signal  | Number | Meaning / Default Action                                 |
| ------- | ------ | -------------------------------------------------------- |
| SIGKILL | 9      | Immediately kills the process (cannot be caught/ignored) |
| SIGTERM | 15     | Politely asks process to terminate (default kill)        |
| SIGINT  | 2      | Interrupt (like pressing Ctrl + C in terminal)           |
| SIGQUIT | 3      | Quit and dump core (like Ctrl + \)                       |
| SIGHUP  | 1      | Hangup – often used to reload config (e.g., daemons)     |
| SIGSTOP | 19     | Stop process (cannot be caught/ignored)                  |
| SIGCONT | 18     | Continue a stopped process                               |
| SIGCHLD | 17     | Sent to parent when child terminates                     |
| SIGSEGV | 11     | Segmentation fault (invalid memory access)               |
| SIGALRM | 14     | Alarm from timer expiry                                  |


## Links:

[[process]]

202509241919