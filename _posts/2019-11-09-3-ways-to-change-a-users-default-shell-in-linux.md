---
layout: article
title:  "Linux: 3 Ways to Change a Users Default Shell in Linux"
date:   2019-11-09 20:30 +0700
tags: shell bash linux chsh
---

## Changing the Default Shell

There are several reasons for changing a user's shell in Linux including the following:

- To [block or disable normal user logins](https://www.tecmint.com/block-or-disable-normal-user-logins-in-linux/) in Linux using a nologin shell.
- Use a shell wrapper script or program to login user commands before they are sent to a shell for execution. Here, you specify the shell wrapper as a user's login shell.
- To meet a user's demands (wants to use  a specific shell), especially those with administrative rights.

When creating user account with the [`useradd` or `adduser`](https://www.tecmint.com/add-users-in-linux/) utilities, the `--shell` flag can be used to specify the name of user's login shell other than that specified in the respective configuration files.

Let's first list all available shells on your Linux system, type:

```
# cat /etc/shells

/bin/sh
/bin/bash
/bin/nologin
/bin/tcsh
/bin/csh
/bin/dash
```

Before you proceed any further, note that:

- A user can change their own shell to anything: which, however must be listed in the `/etc/shells` file.
- Only root can run a shell not listed in `/etc/shells` file.
- If an account has a restricted login shell, then only root can change that user's shell.

### 1. usermod Utility

[usermod](https://www.tecmint.com/usermod-command-examples/) is a utility for modifying a user's account details, stored in the `/etc/passwd` file and the `-s` or `--shell` option is used to change the user's login shell.

First check user account information to view their default login shell and then change the shell from `/bin/sh` to `/bin/bash`.

```
# grep userName /etc/passwd
userName:x:1000:1000:userName,,,:/home/userName:/bin/sh

# usermod --shell /bin/bash userName

# grep userName /etc/passwd
userName:x:1000:1000:userName,,,:/home/userName:/bin/bash
```

### 2. chsh Utility

`chsh` is a command line utility for changing a login shell with the `-s` or `--shell` option like:

```
# grep userName /etc/passwd
userName:x:1000:1000:userName,,,:/home/userName:/bin/bash

# chsh --shell /bin/sh userName

# grep userName /etc/passwd
userName:x:1000:1000:userName,,,:/home/userName:/bin/sh
```

### 3. Change User Shell in /etc/passwd file

This method, simply open the `/etc/passwd` file using any text editor and change a specific users shell.

```
# vim /etc/passwd
```

Source: [3 Ways to Change a Users Default Shell in Linux](https://www.tecmint.com/change-a-users-default-shell-in-linux/)
