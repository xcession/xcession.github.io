---
layout: post
title:  "Vim Motions and Command Language"
date:   2020-01-25 22:44 +0700
categories: vim cheatsheet
---
## Motions and Moving

### Moving within a line

- `h`, `l` - move left/right by character
- `w` - move forward one (w)ord
- `b` - back (b)ackward one word
- `e` - move forward to the (e)nd of a word

### Jumping within a line

- `f<char>` - (f)ind a character forward in a line and move to it
- `T<char>` - find a character backward in a line and move un(t)il it
- `t<char>` - find a character forward in a line and move un(t)il it (one character before)
- `F<char>` - (f)ind a character backward in a line and move to it

- `$` - go to the end of the line
- `0` - go to the beginning of the line

### Moving between lines

- `j`, `k` - move up/down one line
- `H`, `M`, `L` - move (H)igh, (M)iddle, or (L)ow within the viewport
- `Ctrl-u`, `Ctrl-d` - move (u)p or (d)own

- `/` - search for any word in the file
- `n` - repeat last search
- `N` - repeat last search in opposite direction

- `<NN>G` - (G)o to the line number NN

- `G` - go to the end of the file
- `gg` - go to the beginning of the file

## Command Language

Just as any sentence is made up of a verb and a noun, an editing command is made up of two parts: an operation and a section of text. For example, take the command for "delete this word", "change the next sentence" or "copy this parapraph". They all the same structure:

```
<number><command><text object or motion>
```

- The number is used to perform the command over multiple text objects or motions, e.g., backward three words, forward two paragraphs. This number is optional and can appear either before or after the command.
- The command is an operation, e.g, change, delete(cut), or yank(copy).
- The text object or motion can either be a text construct, e.g., a word, a sentence, a paragraph, or a motion, e.g., forward a line, back one page, end of the line.

### Commands

- `d` - (D)elete
- `c` - (C)hange
- `y` - (Y)ank or copy
- `>`, `<` - indent, dedent
- `=` - reformat (reindent, break long lines, etc.)

  The simplest commands are made by repeating the operator a second time to act one the current line. For example, where `d` is the operator for __delete__, `dd` will delete the whole line. Each of `yy`, `cc`, `>>`, `==` behave similarly.

### Using Motions

We can also identify text by using any motion. Just like you can use `w` to move to the next word, you can use `dw` to delete to the next word. This also includes more complex motions such as `t`, which will wait for you to specify a character to go up un(t)il.

- `dw` - delete to the next word
- `dt,` - delete up until the next comma on the current line
- `de` - delete to the end of the current word
- `d2e` - delete to the end of next word
- `dj` - delete down a line (current and below)
- `dt)` - delete up until next closing parenthesis
- `d/rails` - delete up until the first search match for "rails"

### Using Text Objects

You can think of the text object as a kind of "noun" that can be used in place of motions to define a range of text from anywhere within it.

- `iw`, `aw` - inner word, a word
- `ip`, `ap` - inner paragraph, a paragraph
- `i)`, `a)` - inner parenthesis, a parenthesis
- `i'`, `a'` - inner single quote
- `i"`, `a"` - inner double quote
- `it`, `at` - inner tag, a tag

You can also get a full listing from within Vim by typing `:h text-objects`.

Source: [Vim: Motions & Command Language](http://springest.io/vim-motions-and-command-language)
