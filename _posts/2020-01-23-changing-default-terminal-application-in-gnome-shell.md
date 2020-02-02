---
layout: post
title:  "Changing Default Terminal Application in GNOME Shell"
date:   2020-01-23 22:25 +0700
tags: gnome terminal default
---
## Changing Default Terminal Application in GNOME Shell

Ideally, there'd be an option under **Details->Default Applications**, but there's currently no option for "terminal".

So here is a workaround...
Simply symlink the terminal executable of your choice to `gnome-terminal` in `/usr/bin`.

```
$ sudo mv /usr/bin/gnome-terminal /usr/bin/gnome-terminal.bak
$ sudo ln -s /usr/bin/terminator /usr/bin/gnome-terminal
```

Source: [How to change default terminal application in Gnome-Shell](https://askubuntu.com/questions/749832/how-to-change-default-terminal-application-in-gnome-shell#751146)
