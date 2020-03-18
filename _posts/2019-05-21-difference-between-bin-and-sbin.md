---
layout: article
title:  "Linux: Difference Between bin and sbin"
date:   2019-05-21 20:47:32 +0700
tags: filesystem linux
---

# bin and sbin

Ever been curious about the difference between `bin` and `sbin`? The ‘s’ in `sbin` means ‘system’. Therefore, system binaries reside in `sbin` directories.

As you may have noticed, there are a number of different `bin` directories in Linux. The best reference I’ve found for an understanding of various Linux folders is `man hier`. It provides a brief explanation of the [Filesystem Hierarchy Standard (FHS)](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard) in Linux. I’ve included a summary of the various `bin` and `sbin` definitions below:

```
/bin
    This directory contains executable programs which are needed
    in single user mode and to bring the system up or repair it.

/sbin
    Like /bin, this directory holds commands needed to boot the 
    system, but which are usually not executed by normal users.

/usr/bin
    This is the primary directory for executable programs. Most
    programs executed by normal users which are not needed for 
    booting or for repairing the system and which are not
    installed locally should be placed in this directory.

/usr/local
    This is where programs which are local to the site typically
    go.

/usr/local/bin
    Binaries for programs local to the site.

/usr/local/sbin
    Locally installed programs for system administration.
```

If you want to create your own scripts and make them available to all users, you’re pretty safe adding them to `/usr/local/bin`. If you want to run scripts using `cron` or `crontab`, simply use the full path to the command (i.e. `/home/user/command`).

What I do is add my scripts to my local bin (`~/bin`) and then I create a symbolic link in `/usr/local/bin` to the commands I want to make public. As a result, I can manage all my scripts from the same directory but still make some of them publicly available since `/usr/local/bin` is added to `$PATH`.

Source: [Difference Between bin and sbin](http://blog.taylormcgann.com/2014/04/11/difference-bin-sbin/)
