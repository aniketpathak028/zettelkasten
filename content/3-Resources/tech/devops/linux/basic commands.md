---
title: commands
draft: false
tags:
  - linux
  - basics
  - commands
date: 2025-09-23
description: commands
---
# basic commands

- cd "dirname"→ change directory
- pwd → print curr dir
- touch "filename"-> create file
- mkdir "dirname"→ create dir
- rmdir  "dirname"→ remove dir (cannot remove a not empty dir)
- rm -r  "dirname"→ recursively remove (can be used to delete a dir that is not empty)
- rm  "filename"→ remove a file
- man  "command"→ manual for a command
- ls "dirname"→ list (if no dirname lists for pwd)
- ls -a → list hidden files
```bash
ls -alh # a for all files, l for long list, h for human readable
```
- ll → long list
- mv "source_path" "dest_path"→ move a file from source to destination dir, can be used to rename a file incase no destination path is mentioned
- cat "filename"→ read the content of a file or concat the contents of 2 files together
```bash
cat temp2/temp.txt temp2/temp.txt                              
random content...
random content...
```
- w or who-> check user on the system
- top-> list system process and info (mem, ports, pid etc)
- netstat-> list n/w info (tcp, udp connections, and ports)
- cp "src_path" "dest_path"-> copy a file from src → destination
- ">>" - use ">> file path" to write content to the file
### more about htop, top and netstat

## Links:

[[linux]]
[[shell]]

202509230015