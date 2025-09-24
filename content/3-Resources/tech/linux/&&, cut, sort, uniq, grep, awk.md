---
title: "&&, cut, sort, uniq, grep, awk"
draft: false
tags:
  - linux-commands
  - linux
  - grep
  - awk
  - uniq
  - cut
date: 2025-09-24
description: "&&, cut, sort, uniq, grep, awk"
---
# &&, cut, sort, uniq, grep, awk

### &&

>&& is used when we want to perform a series of commands based on the prev command being successful
>
>ex- p1 && p2 && p3 means if p1 is successful only then p2 executes and so forth...

```bash
ls random.txt && cat random.txt
ls: fggfgdsgf: No such file or directory
ls: jjkjklj: No such file or directory
last line
```

### cut

>cut can be used to display content based on a delimiter

```bash
cat random.txt                                             ls: fggfgdsgf: No such file or directory
ls: jjkjklj: No such file or directory
last line

cat random.txt | cut -d: -f2                               fggfgdsgf
jjkjklj
last line
```

>-d can be used to delimit based on a character

>-f can be used to select the index

### sort

>sort can be used to sort based on a condition

```bash
cat random.txt | sort -bf                                  
last line
ls: fggfgdsgf: No such file or directory
ls: jjkjklj: No such file or directory
```

sort items (by alphabetical order, etc.) 
### uniq

only show unique output (duplicates not shown) 
### wc

"word count." Count lines, letters, etc. 
### grep

unbelievably powerful searching/pattern-matching command.

```bash
grep ls random.txt | cut -d: -f1 | uniq                    
```


here for example we’re searching for ls in random.txt and delimiting it based on : and picking the first part of each line and displaying the unique results

</aside>

awk -> text processing command, designed to process structured text data like rows and columns
```bash
awk 'pattern {action}' filename
command | awk 'pattern {action}'
```
built in variables
- $0 -> entire current line
- $1, $2, $3... -> individual fields (columns)
- NF -> number of fields in the current record
- NR -> current record number
- FS - field separator (default - whitespace)
ex- 
```bash
awk '{print $1, $3}' file.txt # print specific columns
awk '/pattern/ {print}' file.txt # print line containing a pattern
awk -F',' '{print $1}' data.csv # custom line separator

cat test.txt
my name is aniket

grep name test.txt | awk -F' ' '{print $1}'
my
```





## Links:

[[linux]]
[[linux-commands]]

202509241042