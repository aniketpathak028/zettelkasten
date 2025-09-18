---
title: vim keybindings
draft: false
tags:
date: 2025-08-21
description: the most useful vim bindings
---
# vim keybindings

By far the most useful key bindings i have been able to learn till now:

### navigation and exit
1. h, j, k, l -> left, down, up, and right
2. :q -> exit vim
3. :q! -> exit vim without saving
4. :wq -> exit vim after saving changes
5. ==gg== -> move to the first line in the file
6. ==shift + g== -> bottom of the file!
7. ==0== -> go to first character of the line
8. ==$== -> last character of the line

### deletion
1. dd -> deletes curr line and copies it to register
2. =={x}dd== -> deletes x lines from curr line
3. ==d + shift + g== -> deletes from the current cursor pos to the end of the file
4. ==dgg== -> deletes everything from bottom line to top!

### copy, paste, redo and undo
1. yy -> cp the line (yank in vim terminology 🙂)
2. {x}yy -> cp x lines from curr line
3. ==:%y+== -> cp entire file in VIM to clipboard
4. p -> pastes copied lines after the cursor
5. u -> undo
6. ctrl + r -> redo changes

### search, replace
1. r  + {whatever you want to replace it with where the cursor is} -> replace at the position where the cursor is
2. / -> search in the file
3. ==:%s/{word to be replaced}/{replacement word}== -> find and replace in the file

### indentation
1. shift + > - shift right
2. shift + < - shift left

### select lines in VIM
- V to select the current line
- j and k to move up or down and select those lines

tips:
1. when you use the --h or help commands on cli or any command that prints a lot of ouput on the screen, pipe it with the less command to use the ouput in the reader and navigate using hjkl 
```bash
k run -h | less
```
2. to search something specific in the cli docs, use the following technique
```shell
k run -h | less
```
then as the docs open press / and the term you want to search for! ex- /dry-run and use the n -> next result and N -> prev result

3. when pasting something from docs into vim, the indentation may get messed up, to correct that when in esc mode use the below command and then in insert mode paste your content to preserve the indentation
```bash
:set paste
```

## Links:

[[neovim]]

202508212317