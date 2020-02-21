---
layout: article
title:  "Kali Linux: Disable Automatic Update (Deprecated)"
date:   2019-07-13 12:46:09 +0700
tags: kali linux update
---

This article is deprecated due to Kali Linux has moved to XFCE4 since version 2019.4.
{:.warning}

## Installing dconf-editor

```
$ sudo apt-get install dconf-editor
```

## Disable the Automatic Update

- Open `dconf-editor`.
- Navigate to **org > gnome > software**.
- Change the **download-updates** key to **false**.

Source: [Kali Linux disable automatic package updates](https://unix.stackexchange.com/questions/240303/kali-linux-disable-automatic-package-updates/327497)

