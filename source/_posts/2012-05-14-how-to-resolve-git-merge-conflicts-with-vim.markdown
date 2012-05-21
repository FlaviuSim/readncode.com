---
layout: post
title: "How to resolve git merge conflicts with Vim"
date: 2011-09-21
comments: true
categories: Programming Vim
permalink: /blog/how-to-do-a-git-merge-with-vim
---

I <3 git. You <3 git. 

We're all coding blazing fast...until you run into a merge conflict

```bash
~/silly-project (master): g merge silly_branch
Auto-merging README.markdown
CONFLICT (content): Merge conflict in README.markdown
Automatic merge failed; fix conflicts and then commit the result.
```

?! git sucks!
You try:

```bash
git mergetool
```

which opens **opendiff** on most macs, and **gvimdiff** on linux. **vimdiff** does not make any sense in this case because it specializes in 2-way-merges, not 3-way-merges. **opendiff** is an ok tool, but it has a GUI, which is soooooo not Vim. 

Here's what you need to do (heavily inspired from **[Drew Neil's screencast](http://vimcasts.org/e/33)**):

-  install the **[fugitive.vim plugin](https://github.com/tpope/vim-fugitive)** (hell, get **[janus](https://github.com/carlhuda/janus)** while you're at it)

-  **vim README.markdown** (instead of using the **mergetool**, just open the conflicted file with Vim)

-  **:Gdiff** (this opens the target/master copy and the merge/branch copy in addition to an attempt at a merged file -- that's what you opened above)

-  In the middle file (future merged file), you can navigate between conflicts with **]c** and **[c**

-  Choose which version you want to keep with **:diffget //2** or **:diffget //3** (the //2 and //3 are unique identifiers for the **target/master** copy and the **merge/branch** copy file names)

-  **:diffupdate** (to remove leftover spacing issues) 

-  **:only** (once you're done reviewing all conflicts, this shows only the middle/merged file)

-  **:wq** (save and quit)

-  **git add .**

-  **git commit -m "Merge resolved"**

-  if you were trying to do a **git pull** when you ran into merge conflicts, type **git rebase --continue**

Hope this helps.

[EDIT] Check out **[Wes's Blog post](http://devblog.policystat.com/blog/using-vim-as-your-git-mergetool/)** on how to integrate **git mergetool** with the steps above.
