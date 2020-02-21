---
layout:	article
title:	"Debian: Basic Commands of apt Package Management"
date:	2019-11-03 13:45:04 +0700
tags: debian apt
---

## What is apt-get

The `apt-get` utility is a powerful and free package management command line program, that is used to work with **Ubuntu's APT (Advanced Packaging Tool)** library to perform installation of new software packages, removing existing software packages, upgrading of existing software packages and even used to upgrading the entire operating system.

## What is apt-cache

The `apt-cache` command line tool is used for searching apt software package cache. In simple words, this tool is used to search software packages, collects information of packages and also used to search for what available packages are ready for installation on **Debian** or **Ubuntu** based systems.

## 1. List All Available Packages

To list all the available packages, type the following command.

```
$ apt-cache pkgnames
```

## 2. Find Out Package Name and Description of Software

To find out the package name nad with it description before installing, use the `search` flag. Using `search` with `apt-cache` will display a list of matched packages with short description.

```
$ apt-cache search vsftpd
```

To find and list down all the packages starting with `vsftpd`, you could use the following command.

```
$ apt-cache pkgnames vsftpd
```

## 3. Check Package Information

For example, if you would like to check information of package along with it short description say (version number, check sums, size, installed size, category etc.). Use `show` sub command as shown below.

```
$ apt-cache show netcat

Package: netcat
Priority: optional
Section: universe/net
Installed-Size: 30
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Original-Maintainer: Ruben Molina <rmolina@udea.edu.co>
Architecture: all
Version: 1.10-40
Depends: netcat-traditional (>= 1.10-39)
Filename: pool/universe/n/netcat/netcat_1.10-40_all.deb
Size: 3340
MD5sum: 37c303f02b260481fa4fc9fb8b2c1004
SHA1: 0371a3950d6967480985aa014fbb6fb898bcea3a
SHA256: eeecb4c93f03f455d2c3f57b0a1e83b54dbeced0918ae563784e86a37bcc16c9
Description-en: TCP/IP swiss army knife -- transitional package
 This is a "dummy" package that depends on lenny's default version of
 netcat, to ease upgrades. It may be safely removed.
Description-md5: 1353f8c1d079348417c2180319bdde09
Bugs: https://bugs.launchpad.net/ubuntu/+filebug
Origin: Ubuntu
```

## 4. Check Dependencies for Specific Packages

Use the `showpkg` sub command to check the dependencies for particular software packages. whether those dependencies packages are installed or not. For example, use the `showpkg` command along with package-name.

```
$ apt-cache showpkg vsftpd

Package: vsftpd
Versions: 
2.3.5-3ubuntu1 (/var/lib/apt/lists/in.archive.ubuntu.com_ubuntu_dists_quantal_main_binary-i386_Packages)
 Description Language: 
                 File: /var/lib/apt/lists/in.archive.ubuntu.com_ubuntu_dists_quantal_main_binary-i386_Packages
                  MD5: 81386f72ac91a5ea48f8db0b023f3f9b
 Description Language: en
                 File: /var/lib/apt/lists/in.archive.ubuntu.com_ubuntu_dists_quantal_main_i18n_Translation-en
                  MD5: 81386f72ac91a5ea48f8db0b023f3f9b

Reverse Depends: 
  ubumirror,vsftpd
  harden-servers,vsftpd
Dependencies: 
2.3.5-3ubuntu1 - debconf (18 0.5) debconf-2.0 (0 (null)) upstart-job (0 (null)) libc6 (2 2.15) libcap2 (2 2.10) libpam0g (2 0.99.7.1) libssl1.0.0 (2 1.0.0) libwrap0 (2 7.6-4~) adduser (0 (null)) libpam-modules (0 (null)) netbase (0 (null)) logrotate (0 (null)) ftp-server (0 (null)) ftp-server (0 (null)) 
Provides: 
2.3.5-3ubuntu1 - ftp-server 
Reverse Provides:
```

## 5. Check statistic of Cache

The `stats` sub command will display overall statistics about the cache. For example, the following command will display Total package names and number of packages have found in the cache.

```
$ apt-cache stats

Total package names: 51868 (1,037 k)
Total package structures: 51868 (2,490 k)
  Normal packages: 39505
  Pure virtual packages: 602
  Single virtual packages: 3819
  Mixed virtual packages: 1052
  Missing: 6890
Total distinct versions: 43015 (2,753 k)
Total distinct descriptions: 81048 (1,945 k)
Total dependencies: 252299 (7,064 k)
Total ver/file relations: 45567 (729 k)
Total Desc/File relations: 81048 (1,297 k)
Total Provides mappings: 8228 (165 k)
Total globbed strings: 286 (3,518 )
Total dependency version space: 1,145 k
Total slack space: 62.6 k
Total space accounted for: 13.3 M
```

## 6. Update System Packages

The `update` command is used to resynchronize the package index files from their sources specified in `/etc/apt/sources.list` file. The update command fetched the packages from their locations and update the packages to newer version.

```
$ sudo apt-get update
```

## 7. Upgrade Software Packages

The `upgrade` command is used to upgrade all the currently installed software packages on the system. Under any circumstances currently installed packages are not removed or packages which are not already installed neither retrieved and installed to satisfy upgrade dependencies.

```
$ sudo apt-get upgrade
```

However, if you want to upgrade, unconcerned of whether software packages will be added or removed to fulfill dependencies, use the `dist-upgrade` sub command.

```
$ sudo apt-get dist-upgrade
```

## 8. Install or Upgrade Specific Packages

The `install` sub command is tracked by one or more packages wish for installation or upgrading.

```
$ sudo apt-get install netcat
```

## 9. Install Multiple Packages

You can add more than one package name along with the command in order to install multiple packages at the same time. For example, the following command will install packages `nethogs` and `goaccess`.

```
$ sudo apt-get install nethogs goaccess
```

## 10. Install Several Packages using Wildcard

With the help of regular expression you can add several packages with one string. For example, we use `*` wildcard to install several packages that contains the `*name*` string, name sould be `package-name`.

```
$ sudo apt-get install `*name*`
```

## 11. Install Packages without Upgrading

Using sub `--no-upgrade` command will prevent already installed packages from upgrading.

```
$ sudo apt-get install packageName --no-upgrade
```

## 12. Upgrade Only Specific Packages

The `--only-upgrade` command do not install new packages but it only upgrade the already installed packages and disables new installation of packages.

```
$ sudo apt-get install packageName --only-upgrade
```

## 13. Install Specific Package Version

Let's say you wish to install only specific version of packages, simply use `=` with the package-name and append desired version.

```
$ sudo apt-get install vsftpd=2.3.5-3ubuntu1
```

## 14. Remove Packages Without Configuration

To uninstall software packages without removing their configuration files (for later re-use the same configuration). Use the `remove` command as shown.

```
$ sudo apt-get remove vsftpd
```

## 15. Completely Remove Packages

To remove software packages inclusing their configuration files, use the `purge` sub command as shown below.

```
$ sudo apt-get purge vsftpd
```

Alternativly, you can combine both the commands together as shown below.

```
$ sudo apt-get remove --purge vsftpd
```

## 16. Clean Up Disk Space

The `clean` command is used to free up the disk space by cleaning retrieved (downloaded) **.deb** files (packages) from the local repository.

```
$ sudo apt-get clean
```

## 17. Download Only Source Code of Package

To download only source code of particular package, use th eoption `--download-only source` with `package-name` as shown.

```
$ sudo apt-get --download-only source vsftpd
```

## 18. Download and Unpack a Package

To download and unpack source code of a package to a specific directory, type the following command.

```
$ sudo apt-get source vsftpd
```

## 19. Download, Unpack and Compile a Package

You can also download, unpack and compile the source code at the same time, using option `--compile` as shown below.

```
$ sudo apt-get --compile source goaccess
```

## 20. Download a Package Without Installing

Using `download` option, you can download any given package without installing it. For example, the following command witll only download `nethogs` package to current working directory.

```
$ sudo apt-get download nethogs
```

## 21. Check Change Log of Package

The `changelog` flag downloads a package change-log and shows the package version that is installed.

```
$ sudo apt-get changelog vsftpd
```

## 22. Check Broken Dependencies

The `check` command is a diagnostic tool. It used to update package cache and check for broken dependencies.

```
$ sudo apt-get check
```

## 23. Search and Build Dependencies

This `build-dep` command searches the local repositories in the system and install the build dependencies for packages. If the package does not exists in the local repository it will return an error code.

```
$ sudo apt-get build-dep netcat
```

## 24. Auto clean Apt-Get Cache

The `autoclean` commane delete all **.dep** files from `/var/cache/apt/archives` to free-up significant volume of disk space.

```
$ sudo apt-get autoclean
```

## 25. Auto remove Install Packages

The `autoremove` sub command is used to auto remove packages that were certainly installed to satisfy dependencies for other packages and but they were now no longer required. For example, the following command will remove an installed package with its dependencies.

```
$ sudo apt-get autoremove vsftpd
```

Source: [25 Useful Basic Commands of APT-GET and APT-CACHE for Package Management](https://www.tecmint.com/useful-basic-commands-of-apt-get-and-apt-cache-for-package-management/)
