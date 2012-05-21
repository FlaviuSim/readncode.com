---
layout: post
title: "View old Git version of a file in a Vim split"
date: 2011-12-25
comments: true
categories: Programming Vim
permalink: /blog/view-old-git-version-of-a-file-in-a-vim-split
---

Wouldn't it be nice if you could view an old version of a file side by side with the current one in Vim? And it would scroll together? And syntax highlight?

Well, open the current file in a Vim window. Then do the following:

1. Open a new (blank) split or window:
```vim
:vsp new
```

2. Dump the old file contents in this new buffer: (note: '!' executes a shell command, and 'read' puts it in the current buffer)
```vim
:read !git show HEAD^:path/to/file/from/root.py
```

3. Set the right syntax highlighting:
```vim
:setf python
```

4. Scroll bind the two splits: (note: you must run this command in both splits)
```vim
:set scrollbind
```

Hope this helps. Let me know if there's a better way to do this.
