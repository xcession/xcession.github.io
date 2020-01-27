---
layout: post
title:  "Vim Buffers, Tabs, Windows and Modes"
date:   2020-01-27 17:10 +0700
categories: vim cheatsheet
---

## Buffers

A buffer in Vim is an __open instance of a file__. This means that the file may not visible on the current screen, but it is saved somewhere in memory.

Whenever you open a file in Vim, that file gets put into buffer that will remain in memory until you explicitly delete it with a call to `:quit` or `:bdelete`. You can list all buffers currently open with a Vim session by typing `:ls`.

- `zz` - Center the current line within the window
- `zt` - Bring the current line to the top of the window
- `zb` - Bring the current line to the bottom of the window

## Windows

A window is Vim is a __viewport onto a single buffer__. You can open a new window with `:split` or `:vsplit`, including a filename in the call. This opens your file as a new buffer (again, similar to a tab in a traditional editor) and opens a new window to display it.

Windows are also referred to a __Splits__.

- `:new <filename>` - Open a new window above the current window
- `:vnew <filename>` - Open a new window beside the current window
- `:split <filename>` - Edit the specified file in new window above the current window
- `:vsplit <filename>` - Edit the specified file in new window beside the current window
- `<Ctrl-w>h, j, k, l` - Navigate to the window in the given direction

## Tabs

A tab in Vim is a __collection of one or more windows__. This allows you to group windows in a useful way.

- `:newtab` - Open a new tab
- `:tabedit <filename>` - Edit the file with the provide name in a new tab
- `gt` - Go to next tab open
- `gT` - Go to previous tab open
- `<Ctrl-w>T` - Break the current window out to a new tab

## Modes

Vim has three different modes: insert, normal and visual.

### Insert Mode

When you use other editors like SublimeText or Atom, you're always working in insert mode. In this mode, character appear immediately in the buffer as you type them. You can enter insert mode by pressing `i` in normal mode.

However, Vim prioritizes moving through a file and making targeted edits, which are done in normal mode.

### Normal Mode

Normal mode is the default mode Vim starts in. You are expected to be in this mode the most of your time, while using all motions and operations.

This fits with the idea that we, as developers, spend the majority of our time moving and editing within document, rather than simply add a long block of text.

### Visual Mode

In more familiar text editor, a block of text can be selected  by clickiing the mouse and dragging over a number of lines or characters. Vim introduces __Visual model__, which allow you to reuse all motion commands and operators that there are to manipulate block of text.

Enter Visual mode by pressing `v` in normal mode. Move the cursor using all the normal motions, and Vim will highlight from where you started to where you move the cursor. You can use a number of keys such as `d`, `x`, or `c` to operate on the visual selection, similar to how these keys would operate in normal mode.

Simetime you will need to operate on entire lines. __Visual Line Mode__ turns out to be very useful in these cases, and it can be started by pressing `V` from normal mode.

But what about selecting a column of text? Vim's got you covered too, enter __Visual Block Mode__ by pressing `<Ctrl-v>` from normal mode.

- `d`, or `x` - Delete the visual block selection
- `c` - Change the visual block selection
- `r` - Replace all characters in the block with the next character you type
- `I` - Insert text before the block
- `A` - Insert text after the block

> Be aware that when you change or add any new text, Vim will only show the change happening in the first line of the block. After you complete the change/insertion and hit `<esc>`, it will replicate to all lines.

## Stay Normal

Avoid staying in insert mode for extended periods of time. And also, don't move along the file while in insert mode. It might be difficult in the beginning, but once you get used to it, you will see how much faster you become. :)

Source: [Vim: Buffers, Tabs, Windows and Modes](http://springest.io/vim-buffers-tabs-windows-and-modes)

