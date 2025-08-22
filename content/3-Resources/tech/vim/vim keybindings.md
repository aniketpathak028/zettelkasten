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
7. 0 -> go to first character of the line
8. $ -> last ch of the line
9. yy -> cp the line (yank in vim terminology 🙂)
10. {x}yy -> cp x lines from curr line
11. :%y+ -> cp entire file in VIM to clipboard
12. p -> pastes copied lines after the cursor
13. u -> undo (v imp)
14. G -> go to last line
15. gg -> go to first line
16. ctrl + r -> redo changes
17. ctrl + B + left bracket + ctrl U -> move up in terminal
18. ctrl + B + left bracket + ctrl D -> move down in terminal

vim tips:
1. when you use the --h or help commands on cli or any command that prints a lot of ouput on the screen, pipe it with the less command to use the ouput in the reader and navigate using hjkl 
```bash
k run -h | less
```





## Links:

[[neovim]]

202508212317