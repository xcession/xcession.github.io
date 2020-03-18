---
layout: article
title:  "macOS: Avoid APFS Conversion on High Sierra Update or Fresh Install"
date:   2019-06-14 22:38:48 +0700
tags: 10.13 apfs high_sierra macos
---

# The APFS on High Sierra

As you already know, macOS High Sierra includes a new file system APFS. If your system drive is solid state, the installer will convert from HFS+J to APFS in both a fresh install scenario and an update scenario.

Fortunately, there a ways around this automatic conversion. It is controlled by the ConvertToAPFS option in `/macOS Install Data/minstallconfig.xml`, which can be controlled by using 'startosinstall' from Terminal, or edited after the fact.

> **Note:** _This guide does not apply to macOS Mojave (or later)._ Apple has removed this option and will force APFS conversion. You can use CCC (Carbon Copy Cloner) to clone from APFS to HFS+J, but that may be a fight you have to take on every update going forward. So,... If you're running Mojave, you will probably end up adopting APFS.

# Update scenario using 'startosinstall'

After downloading the 10.13 installer, instead of running it, quit.

Then in Terminal:

```
$ /Applications/"Install macOS High Sierra.app"/Contents/Resources/startosinstall --converttoapfs NO --agreetolicense
```

The system will copy some files, then reboot, and you'll be able to start the installer (without APFS conversion) by booting the "Boot macOS Install from ..." option in Clover.

# Fresh install scenario (or update) using 'startosinstall'

You _may_ be able to use the startosinstall in the fresh install scenario by invoking it from Terminal after booting the installer from USB. But when I tested it in the betas, it did not work, likely due to a bug in the startosinstall code that prevented it from running from the installer. It seems to be fixed by Apple in later releases of the 10.13 installer.

Terminal is available from the "Utilities" menu within the macOS installer.

If you were to attempt it, the USB installer volume (install_osx if following my guide), appears to be mounted at `/Volumes/"Image Volume"`:

```
$ /Volumes/"Image Volume/Install macOS High Sierra.app"/Contents/Resources/startosinstall --volume the_target_volume --converttoapfs NO --agreetolicense
```

> **Note:** Change `the_target_volume` as appropriate for the actual name you decided to use for your macOS target volume. Hopefully it is obvious that the target volume must already be formatted as HFS+J.

# Fresh install scenario (or update), modifying minstallconfig.xml using PlistBuddy

The process involves creating an installer USB with `createinstallmedia`, then booting that USB (via Clover on the same USB). You then run the installer, create an HFS+J partition suitable for macOS with Disk Utility, then point the installer to that partition.

Even though you create a new HFS+J partition, if the target is an SSD, the installer will still convert it to APFS.

To avoid that, after running the installer, and upon the first reboot where you would be normally directing Clover to boot the next stage of the installer by selecting "Boot macOS Install from ...", instead, boot the "install_osx" partition on USB again. When that is finished booting, choose Terminal from the Utilities menu.

Now, in Terminal, navigate to your target volume:

```
# list /Volumes to remind yourself of the name you gave it
ls -l /Volumes
# then change your working directory to it (in my case, I used '1013')
cd /Volumes/1013
# now change to the "macOS Install Data" directory
cd "macOS Install Data"
# now fix the minstallconfig.xml with PlistBuddy
/usr/libexec/PlistBuddy -c "Set :ConvertToAPFS false" minstallconfig.xml
```

That's it! Now you're ready to quit Terminal, reboot, and continue the installation process by booting the "Boot macOS Install from ..." partition. When you're done, you'll have a fresh install on HFS+J instead of APFS.

# Fresh install scenario (or update), modifying minstallconfig.xml using vi

The process involves creating an installer USB with createinstallmedia, then booting that USB (via Clover on the same USB). You then run the installer, create an HFS+J partition suitable for macOS with Disk Utility, then point the installer to that partition.

Even though you create a new HFS+J partition, if the target is an SSD, the installer will still convert it to APFS.

To avoid that, after running the installer, and upon the first reboot where you would be normally directing Clover to boot the next stage of the installer by selecting "Boot macOS Install from ...", instead, boot the "install_osx" partition on USB again. When that is finished booting, choose Terminal from the Utilities menu.

Now, in Terminal, navigate to your target volume:

```
# list /Volumes to remind yourself of the name you gave it
ls -l /Volumes
# then change your working directory to it (in my case, I used '1013')
cd /Volumes/1013
# now change to the "macOS Install Data" directory
cd "macOS Install Data"
```

Now, still in Terminal, edit the minstallconfig.xml file with vi:

```
vi minstallconfig.xml
```

You will find code:

```
<key>ConvertToAPFS</key>
<true/>
```

Your goal is to change the true to false.

If you know how to use vi, this will not be a problem. Otherwise, follow the instructions below very carefully:
- arrow such that the cursor is at the 't' in 'true'
- press the Del key (forward delete) four times (this removes 'true')
- press i (this puts vi into insert mode)
- type 'false' (without the quotes)
- press Esc (this takes vi out of insert mode)

The result should look like:

```
<key>ConvertToAPFS</key>
<false/>
```

No other changes should be made.

If the file looks good:
- press ':wq' (without the quotes) and press enter (':wq' saves the file and exits vi)

If the file doesn't look right, don't save it:
- press ':q!' (without the quotes) and press enter

That's it! Now you're ready to quit Terminal, reboot, and continue the installation process by booting the "Boot macOS Install from ..." partition. When you're done, you'll have a fresh install on HFS+J instead of APFS.

Source: [Avoid APFS conversion on High Sierra update or fresh install](https://www.tonymacx86.com/threads/guide-avoid-apfs-conversion-on-high-sierra-update-or-fresh-install.232855/)
