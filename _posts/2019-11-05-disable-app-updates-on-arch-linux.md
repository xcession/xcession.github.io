---
layout: article
title:  "Disable App Updates on Arch Linux"
date:   2019-11-05 13:28:51 +0700
tags: linux pacman archlinux
---
Before tinkering around with the `pacman` configuration files to prevent Arch from upgrading a package on your system, you must find the exact name of the package. The best way to do this is by making use of the "`Qe`" command-line switch.

```
$ pacman -Qe
```

This operation will print out a complete list of every installed package on the system.

Running a query of every installed package on Arch Linux will no-doubt show you a lot of information. For most, this vast amount of data may not be helpful. For this reason, it's a good idea to make use of the `grep` command. to sort through and find keywords and patterns.

To sort through your list of installed packages, try:

```
$ pacman -Qe | grep 'name of a program or package'
```

Alternatively, pipe the output to a convenient text file for later with the command below.

```
$ pacman -Qe > ~/package-info.txt
```

> Note: to view the `package-info.txt` file in the terminal, run:

```
$ cat ~/package-info.txt
```

After doing your search with the `grep` tool, you'll see the package name followed by a version number. Ignore the version number and take note of the package name, as you'll need this when editing configuration files.

## Editing `pacman.conf`

The way to prevent Arch Linux from upgrading installed packages is by editing the `/etc/pacman.conf` file and taking advantage of the "`IgnorePkg`" feature. To get to this feature, launch a terminal window and open up the `pacman.conf` file inside of the text editor with root privileges.

Inside the `pacman.conf` make your way down to the part of the file that says "`# Pacman won't upgrade packages listed in IgnorePkg and member of IgnoreGroup`".

Once there remove the `#` symbol from in front of "`IgnorePkg ...`". Then, write in the name of the package from the search earlier after the "`= `".

It should look like:

```
IgnorePkg = nameofpackage
```

Have more than one package you want to prevent Arch Linux from updating? Write out the names of each package followed by commas. For example:

```
IgnorePkg = nameofpackage1, nameofpackage2, nameofpackage3
```

Save changes to the file.

Assuming all edits to `pacman` configuration file are done correctly, you'll be able to run the upgrade command on Arch Linux and successfully prevent the packages in `IgnorePkg` from upgrading.

```
$ sudo pacman -Syyu
```

### Enabling updates

After a few weeks of ignoring an update, it may be safe to upgrade again. To re-enable upgrades for packages that you previously disabled, just edit `/etc/pacman.conf` and remove the package name from "`IgnorePkg`". Then run `pacman` upgrade command.

Source: [How to disable app updates on Arch Linux](https://www.addictivetips.com/ubuntu-linux-tips/disable-app-updates-on-arch/)
