---
layout: article
title:  "macOS: Disable macOS Notification Center"
date:   2017-02-02 11:46:45 +0700
tags: macos notification
---

# Notification Center

Notification Center can be great for reminders, messages and other alerts that you need in order to get through your day unscathed, but if you’re like me, notifications are the devil and they merely just distract you from what you were working on. To disable Notification Center completely, follow these quick steps:

- Open up the **Terminal.app** in **Applications > Utilities**.
- Copy and paste this command into the Terminal window and press Enter:

	`$ launchctl unload -w /System/Library/LaunchAgents/com.apple.notificationcenterui.plist`

- Next, paste this command into Terminal and press Enter:

	`$ killall NotificationCenter`

Notification Center will officially be gone and the little icon will disappear from the menu bar. However, when you two-finger swipe from the right side, it’ll still bring up a gray space marking where Notification Center used to be. To disable this swipe gesture, follow these steps:

- Open up **System Preferences** and click on **Trackpad**.
- Click on the **More Gestures** tab and uncheck **Notification Center**.

Source: [How to Disable Certain Features in OS X](http://www.gottabemobile.com/disable-certain-features-os-x/)
