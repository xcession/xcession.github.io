---
layout: article
title:  "Linux: Basic Linux Filesystem"
date:   2019-07-23 02:37:41 +0700
tags: linux filesystem
---

## The Linux Filesystem

- `/bin` (and `/sbin`) were intended for programs that needed to be on a small `/` partition before the larger `/usr`, etc. partitions were mounted. These days, it mostly serves as a standard location for key programs like `/bin/sh`, although the original intent may still be relevant for e.g. installations on small embedded devices.
- `/sbin`, as distinct from `/bin`, is for system management programs (not normally used by ordinary users) needed before `/usr` is mounted.
- `/usr/bin` is for distribution-managed normal user programs.
- There is a `/usr/sbin` with the same relationship to `/usr/bin` as `/sbin` has to `/bin`.
- `/usr/local/bin` is for normal user programs _not_ managed by the distribution package manager, e.g. locally compiled packages. You should not install them into `/usr/bin` because future distribution upgrades may modify or delete them without warning.
- `/usr/local/sbin`, as you can probably guess at tis point, is to `/usr/local/bin` as `/usr/sbin` to `/usr/bin`.

In addition, there is also `/opt` which is for monolithic non-distribution packages, although before they were properly integrated various distributions put Gnome and KDE there. Generally you should reserve it for large, poorly behaved third party packages such as Oracle.

Source: [/usr/bin vs /usr/local/bin on Linux](https://unix.stackexchange.com/questions/8656/usr-bin-vs-usr-local-bin-on-linux)
