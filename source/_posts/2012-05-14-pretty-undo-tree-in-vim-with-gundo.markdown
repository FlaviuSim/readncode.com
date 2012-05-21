---
layout: post
title: "Pretty undo tree in Vim with Gundo"
date: 2011-12-26
comments: true
categories: Programming Vim
permalink: /blog/pretty-undo-tree-in-vim-with-gundo
---

{% img http://readncode.com/media/images/blog/gundo.png %}

<p></p>Here's a horror story: You make a change in your editor. You undo. You make another change. Crap! You just realized you want the first change, but you can't get it back.

Fortunately, Vim has an undo tree that keeps track of those changes. But it's ugly. So the **[Gundo](http://sjl.bitbucket.org/gundo.vim/)** plugin prettifies it.

If you happen to use [Janus](https://github.com/carlhuda/janus), just add this line to your *~/.janus.rake*

```vim
vim_plugin_task "gundo", "http://github.com/sjl/gundo.vim.git"
```

Then, run *rake* in the *~/.vim* directory to install or update all your Vim plugins (including Gundo).

Don't forget to map a key to toggle the undo tree. The author suggests **F5**, but since Function keys were invented by Kublai Khan, I use the more convenient Leader key + u:

```vim
nnoremap <Leader>u :GundoToggle<CR>
```

Thanks to **[@ciobi](https://twitter.com/#!/ciobi)** for showing me this awesome plugin.
