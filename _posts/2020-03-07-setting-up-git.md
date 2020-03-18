---
layout: article
title:  "Git: Setting Up Git for the First Time"
date:   2020-03-07 17:21:45 +0700
tags: git github config
---

## Setting Up Git for the First Time

After you have Git installed, you need to do few things so that the commit messages that will be generated for you will contain your correct information.

The easiest way of doing this is through the `git config` command. Specifically, we need to provide our name and email address because Git embeds this information into each commit we do. We can go ahead and add this information by typing:

```
$ git config --global user.name "Your Name"
$ git config --global user.name "youremail@domain.com"
```

We can see all of the configuration items that have been set by typing:

```
$ git config --list
```

You can also open the `.gitconfig` file, which contained all of the configuration items. Located in your home directory.

```
$ nano ~/.gitconfig
```

Or by using this command.

```
$ git config --global --edit
```

Source: [How To Contribute to Open Source: Getting Started with Git](https://www.digitalocean.com/community/tutorials/how-to-contribute-to-open-source-getting-started-with-git#check-if-git-is-installed)
