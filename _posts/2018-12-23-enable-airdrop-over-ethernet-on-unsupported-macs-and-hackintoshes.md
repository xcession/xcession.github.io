---
layout: article
title:  "Hackintosh: Enable Airdrop Over Ethernet on Unsupported Macs and Hackintoshes"
date:   2018-12-23 16:23:08 +0700
tags: macos hackintosh airdrop
---

## Enable Airdrop Over Ethernet

Simply enter to following command into Terminal:

```
$ defaults write com.apple.NetworkBrowser BrowseAllInterfaces 1
```

Then, restart Finder by typing "`killall Finder`"

```
$ killall Finder
```

Source: [Enable AirDrop over Ethernet, on Unsupported Macs and Hackintoshes](https://lifehacker.com/5939804/enable-airdrop-over-ethernet-even-on-unsupported-macs-and-hackintoshes)
