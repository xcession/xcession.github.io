---
layout: article
title:  "Linux: Install Parallels Tools or VirtualBox Guest Additions in Linux"
date:   2019-03-20 04:15:13 +0700
tags: virtualbox vbox parallels_desktop linux
---

## Install Parallels Tools or VirtualBox Guest Additions in Linux

Sometimes linux mounts removable media with the `noexec` option, so you cannot execute any files on the CD image. Despite many tutorials telling you to unmount and mount the image again, you can actually remount in one command. Although you do need to get the syntax of the mount command right ;)

```bash
# mount -o remount,defaults,ro,exec /dev/sr0 /media/cdrom
```

The options used are:

- `remount` - remount in place
- `defaults` - because I don't want to bother with all the details
- `ro` - read-only, it's a CDROM
- `exec` - allow execution of files on this mount point.

Source: [Install Parallels Tools in Kali Linux](https://superuser.com/questions/1195551/installing-parallels-tools-in-kali-linux)
