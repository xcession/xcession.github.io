---
layout: article
title:  "macOS: Disable macOS Gatekeeper"
date:   2017-07-27 02:37:03 +0700
tags: macos gatekeeper
---

## Disable Gatekeeper in macOS

The Gatekeeper settings can be found in **System Preferences > Security & Privacy > General**. The Gatekeeper options are located beneath "All apps downloaded from:" with the choice of "Anywhere" missing.

Thankfully, the "Anywhere" setting can be restored to Gatekeeper in Sierra with a Terminal command. First, quit System Preferences if it's open and then open a new Terminal window. Enter the following command, followed by your admin password when prompted:

```
$ sudo spctl --master-disable
```

Now, relaunch System Preferences and head back to the Gatekeeper settings. You'll now see that "Anywhere" has been restored. Click the padlock in the lower-left corner to enter your password and make changes, then select "Anywhere" from the list of Gatekeeper options. The security feature will no longer bug you about apps from unidentified developers.

## Restore Gatekeeper Settings to Default

If you’ve enabled the "Anywhere" option by using the Terminal command above and later want to remove it, you can head back to Terminal and run this command instead:

```
$ sudo spctl --master-enable
```

This way, you can ensure better security for any new users of the Mac.

Source: [How to Disable Gatekeeper and Allow Apps From Anywhere in macOS Sierra](https://www.tekrevue.com/tip/gatekeeper-macos-sierra/)
