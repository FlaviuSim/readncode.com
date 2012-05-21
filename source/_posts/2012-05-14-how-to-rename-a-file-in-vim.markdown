---
layout: post
title: "How to rename a file in Vim"
date: 2011-11-10
comments: true
categories: Programming Vim
permalink: /blog/how-to-rename-a-file-in-vim
---

We've all had to **mv** a file from the Terminal when we wanted to rename it.

But what if you have the buffer open in Vim already? Vim has a **:saveas [new_file]** , but it does not delete the old file.

Meet the **[Rename Vim Plugin](http://www.vim.org/scripts/script.php?script_id=1928)**:

```vim
:rename <newfile>
```vim

Yup, that is all you have to type in Vim to rename a file.

However, if you want to use Rename with the **[Janus collection of plugins](https://github.com/carlhuda/janus)**, you'll need to install **Rename** using the **[github link](https://github.com/wojtekmach/vim-rename)**

Just add this to your **~/.janus.rake**

```vim
vim_plugin_task "rename", "https://github.com/wojtekmach/vim-rename.git"
```vim

Then, run **rake** in your **~/.vim/** directory, and all the plugins will install.

Yay!
