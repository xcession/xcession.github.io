---
layout: post
title:  "pacman unable to lock database"
date:   2019-09-05 21:01 +0700
tags: archlinux pacman
---
## Cause of the problem

Such as system crashed or power shortage while the `pacman` is still running. This cause the file `db.lck` is still present.

## The "db.lck" file

The **db.lck** file is located in `/var/lib/pacman/db.lck`. Remove this file to solve this problem.

Source: [pacman: "unable to lock database"](https://bbs.archlinux.org/viewtopic.php?id=149042)
