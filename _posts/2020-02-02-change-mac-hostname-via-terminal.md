---
layout: post
title:  "Change Mac Hostname via Terminal"
date:   2020-02-02 20:46 +0700
tags: mac macos terminal hostname
---

Launch the terminal application in macOS and then use the following command syntax:

```
$ sudo scutil --set HostName new_hostname
```

## Another Method for Setting the Mac Hostname

With modern macOS releases from macOS Mavericks and newer, you can also use the `hostname` command with a flag to set the hostname to be permanently changed:

```
$ sudo hostname -s YourHostName
```

## Checking the Current Mac Hostname from the Command Line

After the above command is executed you can verify that the changes took place by typing:

```
$ hostname
```

## Setting a Temporary Hostname Change

You can also set a __temporary hostname change__ by using the following command:

```
$ sudo hostname new_hostname
```

Source: [Change you Mac Hostname via Terminal](http://osxdaily.com/2010/09/06/change-your-mac-hostname-via-terminal/)

