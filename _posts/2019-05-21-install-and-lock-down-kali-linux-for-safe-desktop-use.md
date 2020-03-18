---
layout: article
title:  "Kali Linux: Install & Lock Down Kali Linux for Safe Desktop Use"
date:   2019-05-21 16:06:37 +0700
tags: kali linux
---

# Install & Lock Down Kali Linux for Safe Desktop Use

Kali Linux is established as the go-to operating system for penetration testing, but it's default configuration, it's less than ideal for regular desktop use. While in many scenarios, a live boot or virtual environment can resolve these issues, in some situations, a full installation is better. A few simple changes can be made to Kali Linux desktop to make it safer to use in this environment.

Kali, unlike other Linux distros, is designed with the sole intention of acting as a penetration test toolkit. This means that while the desktop-focused tools such as office suites and games are bny no means neglected, they are not the focus of the developers. The distro is primarily configured for temporary use, shown in the way it defaults to a single-user mode, a choice which would go against security best practics for a desktop-focused distribution. There are a few other common ways to use Kali besides installing it in the way of traditional operating system.

The most convenient way to use Kali is likely by [running it within a virtual machine](https://null-byte.wonderhowto.com/how-to/mac-for-hackers-install-kali-linux-as-virtual-machine-0174250/). Tools like VirtualBox allow one to use other operating systems within a sandbox environment on a Windows, macOS, Linux, or BSD host operating system. The limitations of a virtual machine include potentially difficult configuration, higher  memory usage, slower performance, and problems interfacing with network hardware. Some of these issues may be resolved by running Kali as a live boot.

Using Kali as a live boot means creating a booting disk image on an external drive and booting from device rather than the operating system installed on the hard drive of a system. This allows direct access to the system and network hardware, as the additional layer of a host OS used for virtualization can be bypassed. Kali also provides persistent and encrypted live image options, meaning that any work done within a live setup can be saved to the same drive. While this persistent makes Kali very useful as a live system, system performance and storage space can become an issue.

If neither of these, Kali can also be [run as a Windows subsystem](https://null-byte.wonderhowto.com/how-to/run-kali-linux-as-windows-subsystem-0181914/), If you'd like to continue using Windows without the need for even a reboot, nor a full virtual machine environment.

Kali is by no means recommended or ideal for primary desktop usage. To quote the [Kali Linux documentation](https://docs.kali.org/introduction/should-i-use-kali-linux):

> The fact of the matter is, however, that Kali is a Linux distribution specifically geared towards professional penetration testers and security specialists, and given its unique nature, it is not a recommended distribution if you're unfamiliar with Linux or are looking for a general-purpose Linux desktop distribution for development, web design, gaming, etc.

If you do, however, choose to install Kali Linux, there are a few steps which can be taken to make it more practical for regular desktop usage as well as penetration testing. This can be useful for longer projects, producing documentation or reports during an engagement, or for limiting the number of operating systems and partitions one may need on a given system.

# Configuring User Accounts

In the default Kali configuration, the operating system is single-user. This user account is the root account, or superuser account, designed on most systems to separate privileges such that only one user account is able to do certain tasks. On Kali, this is convenient for most usage as there is no need to switch between users.

On a regular desktop-focused Linux distribution, these privileges are separated for security reasons. When running as an unprivileged user, any tasks run or tools installed will need to be specifically granted these privileges each time they are used. This greatly limits the posibility of abuse or misuse.

If you intend to use Kali as anything other than purely a penetration testing toolkit, it may be worth you time to configure a separate unprivileged user account. If you run [`whoami`](https://null-byte.wonderhowto.com/how-to/hack-like-pro-linux-basics-for-aspiring-hacker-part-1-getting-started-0147121/) on a default Kali installation, you'll see that you are running as the root user.

```
root@kali:~# whoami
root
root@kali:~# _
```

While running as root is not good security practice for a desktop distro, it will simplify the process of creating a new user. To begin creating a new account, run the command below, replacing "new-username" with the name of the new user you would like to create.

```
# adduser -m new-username
```

This will create a new user account, as well as a new home directory for the user. We ca confirm the existence of the new directory by running [ls](https://null-byte.wonderhowto.com/how-to/hack-like-pro-linux-basics-for-aspiring-hacker-part-2-creating-directories-files-0147234/) `/home/`.

```
root@kali:~# ls /home/
new-username
root@kali:~# _
```

Next, we can set a password for this newly created user account. This password should be different than your root password. To set it, run the command below, replacing "new-username" with the username of the account you previously created.

```
# passwd new-username
```

After running this command, you will be prompted to type and retype you new password.

```
root@kali:~# passwd new-username
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
root@kali:~# _
```

Once a user account and password are created, we can set privileges for the new account. The main change we'll make is adding the user to the "Sudoers" user group. This group allows any user within it to utilize Sudo, which allows them to run commands as other users. The name of the tool originally stood for "superuser do" but now is generally to be run as other users, besides just root. In the case of Kali, Sudo will generally be used to run commands which require root privileges while running as an unprivileged user.

To add the newly created user to the "sudo" user group, one can run the command below, replacing "new-username" with the username of the user you would like to add.

```
root@kali:~# useradd -aG sudo new-username
root@kali:~# _
```

After this user is created, one can log out and log back into the user account from the main Kali login screen. To do this, simply type the username of the new user rather than that of the root account.

Once logged in, one can open a new terminal window, and upon running `whoami`, see the username of the new user account. In this new terminal window, it may also be noted that the shell in use appears slightly different from the root user shell. This is because the shell for the new user has not yet been set to BASH. To set it, run the command below, replacing "new-username" with your account name.

```
$ whoami
new-username
$ chsh -s /bin/bash new-username
Password:
$ _
```

Now that a new user account and shell has been configured, the account is ready to use! Commands you wish to run as root can be prefaced with `sudo` when running as a standard user, maintaining the security and isolation of privileges provided by most standard Linux desktops.

# Changing Network Service Policies

As stated in the [Kali documentation](https://docs.kali.org/policy/kali-linux-network-service-policies), "Kali Linux deals with network services in a very different way than typical Linux distributions. Specifically, Kali does not enable any externally-listening services by default with the goal of minimizing exposure when in a default state." These changes mean that Kali "will disallow network services from persisting across reboots by default."

This means that certain network services you choose to install may initially work, but then mysteriously fail during reboots. While it's possible to manually start these services using the "systemctl" component of Systemd, if you would like for a service to persist through reboots, you'll need to edit the whitelist/blacklist.

To edit this file using Nano, you can run the command below.

```
$ sudo nano /usr/sbin/update-rc.d
```

While the beginning of the file looks more like a Perl script than a whitelist, scrolling further into the file, one can see a section specifically for the whitelist and blacklist.

If you have a service you'd like to add to the whitelist, first ensure that it is not included in the blacklist section of the file. If it is, remove the line before continuing. To add a new entry, simply type the name of the service followed by **enabled** on a line within the whitelist section.

After you are done editing this file, you can save your changes by pressing `Ctrl+O` and exit with `Ctrl+X`. Any changes which are made to startup initialization services should take effect on the next reboot.

# Enable Kali Rolling

After installing Kali, you should check your repository sources to ensure that the correct address is set. Run the command below to edit the file in Nano.

```
$ sudo nano /etc/apt/sources.list
```

Confirm that the file includes the line below and that it is not commented out by a # symbol at the beginning of the line.

```
deb http://http.kali.org/kali kali-rolling main non-free contrib
```

After ensuring this line is present or adding it to the file, press `Ctrl+O` and then press `Ctrl+X` to save changes.

After this file is updated, you can update the system, or choose to upgrade it. First, run the `apt-get` command below to update the repositories.

```
$ sudo apt-get update
```

If you wish to perform a full system upgrade and install the newest version of all installed software, you can also choose to run the command below.

```
$ sudo apt-get upgrade
```

Once you repositories are updated and the system is up to date, you can also begin to install additional software to further configure your Kali installation.

Source: [Install & Lock Down Kali Linux for Safe Desktop Use](https://null-byte.wonderhowto.com/how-to/install-lock-down-kali-linux-for-safe-desktop-use-0184531/#jump-step2)
