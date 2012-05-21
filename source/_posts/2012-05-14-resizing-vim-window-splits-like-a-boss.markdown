---
layout: post
title: "Resizing Vim window splits like a boss"
date: 2011-10-09
comments: true
categories: Programming Vim
permalink: /blog/resizing-vim-window-splits-like-a-boss
---

If you're using Vim as your text editor (if you're not, **<a href="http://www.derekwyatt.org/vim/vim-tutorial-videos/vim-novice-tutorial-videos/#Welcome" target="_blank">these videos</a>** will convince you), you're probably using window splits.

If you're using window splits, you probably wished you had a quick way to resize them.

I recently watched Gary Bernhardt's video on **<a href="https://www.destroyallsoftware.com/screencasts/catalog/file-navigation-in-vim" target="_blank">VIM File Navigation</a>**, and got inspired to research this problem.

So, set the following in your **~/.vimrc**:

```vim
set winheight=30
set winminheight=5
```


This will make sure all splits will be at least 5 lines (which is enough for reference), and the current window will be 30 lines. As you navigate through the windows, the current one will become 30 lines.

You can increase or decrease the size of a window by one line with **Ctrl-w** + **-** and **Ctrl-w** + **+**.

That probably makes no sense. So you should use **+** and **-** to increase or decrease windows by a sane amount:

```vim
nnoremap <silent> + :exe "resize " . (winheight(0) * 3/2)<CR>
nnoremap <silent> - :exe "resize " . (winheight(0) * 2/3)<CR>
```

As for navigation, I'm using these mappings to move between splits with **Ctrl-w** + **-** and **Ctrl-w** + **+*:

```vim
nnoremap <C-h> <C-w>h
nnoremap <C-j> <C-w>j
nnoremap <C-k> <C-w>k
nnoremap <C-l> <C-w>l
```

Also, if you want to make all windows equal, use **Ctrl-w** + **=**

Check **<a href="http://vim.wikia.com/wiki/Resize_splits_more_quickly" target="_blank">this</a>** out for similar nuggets.

