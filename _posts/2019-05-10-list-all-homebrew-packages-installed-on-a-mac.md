---
layout: article
title:  "macOS: List All Homebrew Packages Installed on a Mac"
date:   2019-05-10 20:26:57 +0700
tags: macos homebrew brew.sh
---

## List All Homebrew Installed Packages

Homebrew includes a simple and convenient command to list all packages that have been installed through brew, the syntax is as follows:

```
$ brew list
```

Sample output may look something like the following, depending on what packages and their dependencies you have installed:

```
$ brew list
bash-completion gettext libidn2 pcre watch
cask glib libunistring pcre2 wget htop links python nmap irssi node smartmontools libffi openssl sqlite
```

You may have fewer or more brew packages installed, depending on your particular setup.

It can also be helpful to export the list of Homebrew packages that are installed into a text file, that can be done by redirecting the output of brew list into a plain text file like so:

```
$ brew list > homebrewpackages.txt
```

The output would be the same, but now its stored in the “homebrewpackages.txt” file which you could share with someone else or document for other purposes.

## How to List All Cask Homebrew Packages on Mac

```
$ brew cask list
```

If you issue that command and nothing comes back, that simply means you have not installed any Mac apps through brew cask, which is not a terribly unusual situation as many Mac users just use Homebrew for command line tools and binaries and not for maintaining other Mac apps. Nonetheless cask remains a very popular method to easily install, maintain, and manage various Mac apps as well. It really just depends on the individual users particular setup.

As hinted in the introduction to this article, another method of finding what Homebrew packages are installed on a Mac by simply using the ls command to [show where Homebrew packages are installed](http://osxdaily.com/2018/07/05/where-homebrew-packages-installed-location-mac/):

```
$ ls /usr/local/Cellar/
```

The output of that command will be every package installed through Homebrew, as they always end up in that directory by default.

## How do I find what Homebrew packages are available to install?

Obviously we’re focusing on what Homebrew packages are currently installed on a Mac, but if you want a list of Homebrew packages that are available to install instead then you can use either of the following methods. The first approach uses a simple search command:

```
$ brew search
```

The output of ‘`brew search`’ will be every available Homebrew package that could be installed.

Or you can browse [the brew formula page here](https://formulae.brew.sh/formula/) for a full list of Homebrew packages that could theoretically be installed.

Source: [How to List All Homebrew Packages Installed on a Mac](How to List All Homebrew Packages Installed on a Mac)
