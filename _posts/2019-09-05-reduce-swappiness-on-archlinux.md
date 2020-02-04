---
layout: article
title:  "Arch Linux: Reduce Swappiness"
date:   2019-09-05 21:00 +0700
tags: archlinux manjaro swap
---

## Reducing Swappiness

**Swappiness** is to optimize the use of Swap and RAM. And it allows establishing the balance between both. By default when Arch Linux uses a lot of the RAM memory it starts writing some files into the Swap partition on your hard drive. The problem with this is the hard disk is slower than the RAM, soo this makes the system slower. You can reduce the use of Swap and use more RAM instead.

First, check the default swappiness value. Run in a terminal:

```
$ cat /proc/sys/vm/swappiness
```

The default value is `60`, which is too conservative. So recommend changing the value to `10` if you have more than 4GB of RAM. To do this you need to create the file `/etc/sysctl.d/100-manjaro.conf`. Run this command:

```
$ sudo nano /etc/sysctl.d/100-archlinux.conf
```

In the file, you have to put the following:

```
vm.swappiness=10
```

Then save the file.

In order for the changes to take effect, reboot the system.

Then, check the swappiness value again:

```
$ cat /proc/sys/vm/swappiness
```

And you'll see it's `10`. So this way Arch Linux will use your RAM memory more efficient.

Source: [10 things to do after installing Manjaro](https://averagelinuxuser.com/10-things-to-do-after-installing-manjaro/)
