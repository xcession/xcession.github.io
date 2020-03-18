---
layout: article
title:  "Hackintosh: New Method for Enabling Nvidia Web Drivers in Clover"
date:   2017-07-27 03:44:15 +0700
tags: macos hackintosh clover nvidia driver
---

# Enabling Nvidia Web Drivers

As of **macOS Sierra**, ```nvda_drv=1``` in **config.plist** under **Boot > Arguments** is no longer working to initiate drivers. Clover has been updated with a new System Parameter setting called **NvidiaWeb**.

-  Mount EFI Partition
-  Open **/Volumes/EFI/EFI/CLOVER/config.plist** with text edit, Xcode, or Plist Editor Pro
-  Edit as shown below:

```
<key>SystemParameters</key>
    <dict>
        <key>InjectKexts</key>
        <string>YES</string>
        <key>InjectSystemID</key>
        <true/>
        <key>NvidiaWeb</key>
        <true/>
    </dict>
```

- Remove **Boot/Arguments/nvda_drv=1** if necessary
- Save and reboot

Source: [New Method for Enabling NVIDIA Web Drivers in Clover](https://www.tonymacx86.com/threads/new-method-for-enabling-nvidia-web-drivers-in-clover.202341/)
