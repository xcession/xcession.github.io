---
layout: article
title:  "tmux: Change Default tmux Key Binding"
date:   2019-10-11 22:14:02 +0700
tags: tmux terminal
---

# Changing tmux Default Key Binding

Bt default, command key bindings are prefixed by `ctrl+b`. For example, to vertically split a window type `ctrl+b %`.

After splitting a window into multiple panes, a pane can be resized by the hitting prefix key (e.g. `ctrl+b`) and, while continuing to hold `ctrl`, press `left/right/up/down`. Swapping panes is achived in the same manner, but by hitting `o` instead of a directional key.

Key bindings may be changed with the bind and unbind commands in `tmux.conf`. For example, the default prefix binding of `ctrl+b` can be changed to `ctrl+a` by adding the following commands in your configuration file:

```
unbind C-b
set -g prefix C-a
bind C-a send-prefix
```

> **Tip:** Quote special characters to use them as prefix. You may also use `alt` (called Meta) instead of `ctrl`. For example: `set -g prefix m-'\'`

Source: [tmux - ArchWiki (Key bindings)](https://wiki.archlinux.org/index.php/Tmux#Key_bindings)
