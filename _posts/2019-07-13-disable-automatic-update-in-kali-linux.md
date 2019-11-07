---
layout: post
title:  "Disable Automatic Update in Kali Linux"
date:   2019-07-13 12:46 +0700
categories: kali linux update
---
## Installing `dconf-editor`

```
$ sudo apt-get install dconf-editor
```

## Disable the Automatic Update

- Open `dconf-editor`.
- Navigate to **org > gnome > software**.
- Change the **download-updates** key to **false**.

Source: [Kali Linux disable automatic package updates](https://unix.stackexchange.com/questions/240303/kali-linux-disable-automatic-package-updates/327497)
