---
layout: article
title:  "Linux: How to Block or Disable Normal User Logins in Linux"
date:   2019-11-09 20:46 +0700
tags: shell linux chsh login
---

## How to Block User Logins Using /etc/nologin File

The primary function of `/etc/nologin` file is to display a message (stored in the file) to users attempting to log on to a system during the process of shutdown.

Once the message has been displayed to the user, the login procedure terminates, preventing the user from logging on to system.

This can be used to block user login by manually creating the file as follows:

```
# vim /etc/nologin
```

Add the message below to the file, which will be shown to users attempting to log on to the system.

```
The Server is down for a routine maintenance. We apologize for any inconvenience caused, the system will be up and running in 1 hours time. For more information, contact admin admin@system.com.
```

Now a normal user is not able to login.

## How to Bloack User Logins Using nologin Shell

This method works a little differently: it only blocks a user from accessing a shell. But they can log on to the system via programs such as `ftp` that do not necessarily require a shell for the user to connect to a system.

Additionally, it can allow you to block shell access to specific users in special scenarios.

Simply use `chsh` (change shell) command to change the users shell in `/etc/passwd` file from something like `/bin/bash` or `/bin/sh` to `/sbin/nologin`.

```
# chsh -s /sbin/nologin userName
```

### On Ubuntu or Debian Based Distributions

Here, you have to use `/bin/false` file.

```
$ sudo chsh -s /bin/false userName
```

Source: [How to Block or Disable Normal User Logins in Linux](https://www.tecmint.com/block-or-disable-normal-user-logins-in-linux/)
