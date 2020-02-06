---
layout: article
title:  "macOS: Turn Off Rootless (SIP or System Integrity Protection)"
date:   2017-07-27 02:43 +0700
tags: macos sip rootless
---

## Turning Off SIP

Apple introduced System Integrity Protection (rootless) mode as a security feature in OS X El Capitan. It prevents you (and programs) from changing root-level files even with your password, but it can stop some programs from working. Here's how to disable it

## How to turn off rootless/System Integrity Protection on Mac: Disable SIP

- Turn off your Mac (**Apple > Shut Down**).
- Hold down **Command-R** and press the Power button. Keep holding **Command-R** until the Apple logo appears.
- Wait for OS X to boot into the OS X Utilities window.
- Choose **Utilities > Terminal**.
- Enter ```csrutil disable.```
- Enter reboot.

Your Mac will reboot and start up with SIP disabled. You can check the status of SIP by opening Terminal and entering ```csrutil status```. You should see "System Integrity Protection status: disabled."

## How to turn on rootless/System Integrity Protection on Mac: Switch SIP back on

- Turn off your Mac (**Apple > Shut Down**).
- Hold down **Command-R** and press the Power button. Keep holding **Command-R** until the Apple logo appears.
- Wait for OS X to boot into the OS X Utilities window.
- Choose **Utilities > Terminal**.
- Enter ```csrutil enable```.
- Enter reboot.

Now open Terminal and enter ```csrutil status``` to check the status of SIP. It should say "System Integrity Protection status: enabled."

Source: [How to turn off Rootless (SIP, or System Integrity Protection) in Mac OS X](http://www.macworld.co.uk/how-to/mac/how-turn-off-mac-os-x-system-integrity-protection-rootless-3638975/)
