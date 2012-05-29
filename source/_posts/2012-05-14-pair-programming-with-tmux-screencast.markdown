---
layout: post
title: "Pair Programming with Tmux Screencast"
date: 2012-02-18
comments: true
categories: Hacking Programming Screencast
permalink: /blog/pair-programming-with-tmux-screencast
---

<iframe width="420" height="315" src="http://www.youtube.com/embed/za8FMIWYtUc" frameborder="0" allowfullscreen></iframe>

Notes/Links:
  
<a href="http://tmux.sourceforge.net/" target="_blank">Tmux Home</a>

<a href="http://www.openbsd.org/cgi-bin/man.cgi?query=tmux" target="_blank">Man Page</a>

<a href="http://peterc.org/blog/2010/216-tmux.html" target="_blank">Screencast by Peter Cooper</a>

<a href="http://smartic.us/2010/11/30/a-tmux-rant-or-a-drunken-ramble-by-bryanl-you-pick/" target="_blank">Tmux Rant y Bryan Liles</a>

Funny, <a href="http://thechangelog.com/post/17827235767/episode-0-7-3-tmux-with-brian-hogan-and-josh-clayton" target="_blank">the changelog episode this week</a> also covered tmux. So, check it out.

My ~/.tmux.conf

```
# use vi mode
setw -g mode-keys vi

# remap prefix to Control + a
set -g prefix C-a
unbind C-b
bind C-a send-prefix

# force a reload of the config file
unbind r
bind r source-file ~/.tmux.conf

# quick pane cycling with Ctrl-a
unbind ^A
bind ^A select-pane -t :.+

# move around panes like in vim (only in tmux 1.6)
bind j select-pane -D
bind k select-pane -U
bind l select-pane -R
bind h select-pane -L

# Sane scrolling
set -g mode-mouse on
```

Also, note that Ctrl-A D will let you view and detach other clients. :)
