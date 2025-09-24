---
title: pipes and redirections
draft: false
tags:
  - pipes
  - redirection
  - linux
date: 2025-09-23
description: pipes and redirections
---
# pipes and redirections

a STDIN, STDOUT could be a shell/keyboard/network!

3 std streams in linux:

- STDIN —> descriptor-0 (the command reads its input from)
- STDOUT —> descriptor-1 (the command writes its normal output to)
- STDERR —> descriptor-2 (the command writes its error to)

Output redirection (> and >>)
```bash
echo "hello world" 1> random.txt # 1> stdout redirect
cat random.txt                                                               hello world
```
```bash
ls fggfgdsgf 2> random.txt # 2> stderr redirect
cat random.txt
ls: fggfgdsgf: No such file or directory
```

> ">" overwrites the file all the time! use ">>" to append lines to the file without overwriting

```bash
ls jjkjklj 2>> random.txt  # appends to the file                             
cat random.txt                                                               
ls: fggfgdsgf: No such file or directory
ls: jjkjklj: No such file or directory
```

>"<" is used to input something from a file, for ex sending the contents of a file in an email

```bash
mail -s "cli email" aniket < random.txt
```

> the pipe “|” command in linux is a very useful command that can be used to hook up the output of one command into the input of another one! ex- listing all processes with pagination.

```bash
p1 | p2 | p3 # p1 o/p -> p2 -> p2 o/p -> p3 -> p3 o/p -> STDOUT
```

```bash
ps aux | less
```

> Note:
> date | echo "date is :" will not pass the output of the date command to the echo command because date is a system default command passing the output to STDIN while echo only reads the STDOUT

commands which read STDIN- cat, grep, sed, awk, sort, wc
commands which read STDOUT- echo, ls, date, pwd
## Links:

[[linux]]
[[shell]]

202509231139