---
title: vim keybindings
draft: false
tags:
date: 2025-08-21
---
# vim keybindings

By far the most useful key bindings i have been able to learn till now:

1. h, j, k, l -> left, down, up right navigation!
2. :q -> exit vim 💀
3. :q! -> exit vim without saving
4. :wq -> exit vim after saving changes
5. dd -> deletes curr line and copies it to register
6. {x}dd -> deletes x lines from curr line
7. gg -> move to the first line in the file
8. dG -> deletes from the current cursor pos to the end of the file
9. dgg -> deletes everything from bottom line to top!
10. 0 -> go to first character of the line
11. $ -> last ch of the line
12. yy -> cp the line (yank in vim terminology 🙂)
13. {x}yy -> cp x lines from curr line
14. :%y+ -> cp entire file in VIM to clipboard
15. p -> pastes copied lines after the cursor
16. u -> undo (v imp)
17. G -> go to last line
18. gg -> go to first line
19. ctrl + r -> redo changes
20. ctrl + B + left bracket + ctrl U -> move up in terminal
21. ctrl + B + left bracket + ctrl D -> move down in terminal
22. shift + G -> bottom of the file!
23. d + shift + G -> delete until the end of the file!

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
3. when pasting something from docs into vim, the indentation may get messed to correct that when in esc mode use the below command and then in insert mode paste your content to preserve the indentation
```bash
:set paste
```





## Links:

[[neovim]]

202508212317