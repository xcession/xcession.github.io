---
layout: article
title:  "Speed Up Command Line Navigation"
date:   2020-03-30 10:54:37 +0700
tags: commandline terminal
---

# Speed Up Command Line Navigation

## Run That Again as Root — sudo !!

```
user@host: cat /var/log/messages
cat /var/log/messages: Permission denied.
```

**Don't type:** Up. Left. Left. Left.... `sudo` Enter.

**Instead:** `sudo !!`

This is a little shortcut works, because `!!` is a shell place holder for the last command executed. Typing these 7 characters will run that last command as root without those Up and Left keypresses. Equally this shortcut works without `sudo`, if you want to run the last command again without changes, for some reason.

## Re-type That Last Argument — Alt+.

Dis you want to use that last argument you just typed? The directory you just created?

**Don't type:** `mkdir newdirectory; cd newdirectory`

**Instead:**

```
mkdir newdirectory
cd <Alt+.>
```

## Search for That Command I Ran — Ctrl+R

What was that command I ran? Up. Up. Up. Up. Oh there it is.

**Don't type:** Up. Up. Up. Enter.

**Instead:** Ctrl+R

Simply tap 'Ctrl+R', and type the first few letters of the command you wanted. If the search doesn't match on the first result, just tap `Ctrl+R` a few more times to scroll through result.

## Go Back to You Home Directory — cd

You would be amazed how many people don't know this. `cd`. That's right. Without any arguments. it takes you back to your home directory.

## Go Back to the Last Directory — cd -

Sometimes the simplist things are the best. Where you in the `/var/www/foo` directory, but are now in `/etc`? Simply `cd -` will take you back to `/var/www/foo`.

**Don't type:** `cd /var/www/foo`

**Instead:** `cd -`

## Job Control — Backgrounding, Foreground, Etc

This might take some getting used to, but when you get the hang of it you'll never go back. Let's say you are editing a file in `vim` (well, you wouldn't use `nano`, would you?!), and now you want to go and look in the `/var/www/html` directory. You could quit vim, browse to the directory, only to find that you want to edit the file again. Instead, you can send vim to background and come back to it later.

**Type:** `Ctrl+Z` — This is a shortcut that backgrounds any existing foreground task. Useful for, but not limited to; `less`, `cat`, `man`, `vim`, etc.

Where did my foreground task go, you might ask. Simply type `jobs` to see it in a list.

```
user@host: jobs
[1] Stopped         vim
```

Great. You can now go do something else. whenever you want this back again, simply, type `fg`. This will bring the background job (vim) back again. Note that the process is paused, so if you're running something like `tail` on a file, the process will have some catching up to do. If you have multiple jobs running in the background `fg 3`, for example, will resume the 3rd job. Don't forget to run the `jobs` command to see a list.

## Alias the stuff you use frequently — eg netstatx

If you run a command with the same arguments nearly all the time, create a "shortcut" alias for this — I have many of them. I often use the `<commandname>x` syntax — ie, the command's normal name followed by an x. For example, with `netstat`, I always run it with `-n` (numeric addresses only), `-t` (tcp protocol), `-a` (all), `-u` (udp protocol), and `-e` (extended output). `netstat -ntaupe` — it rolls right off tounge. I'm lazy though (and might forget an option), so I aliased that to `netstatx` like this;

```
alias netstatx="netstat -ntaupe"
```

Try it for anything you run regularly.

**Don't type:** `netstat -ntaupe`

**Instead:** `netstatx` (or whatever command you use often!)

Source: [Speed Up Your Command Line Navigation](https://medium.com/james-reads-public-cloud-technology-blog/speed-up-your-command-line-navigation-d4050207f02c)
