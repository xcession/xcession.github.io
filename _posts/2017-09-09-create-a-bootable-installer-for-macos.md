---
layout: post
title:  "Create a bootable installer for macOS"
date:   2017-09-09 15:45 +0700
tags: macos installer usb flashdrive bootable
---
> With macOS Sierra, El Capitan, Yosemite, or Mavericks, you can use a USB flash drive or other removable media as a startup disk from which to install the Mac operating system.

These advanced steps are intended primarly for system administrators and others who are familiar with the command line. Make sure you use a USB flash drive or other removable media that has at least 12GB of available disk space.

## Use the 'createinstallmedia' command in Terminal

- Download the macOS installer from the Mac App Store. Quit the installer if it opens automatically after downloading. The installer will be in your **Applications** folder.
- Mount your USB flash drive or other volume. You could also use a secondary internal partition that has at least 12GB of available disk space for the installation files.
- Open the **Terminal.app**, which is in the **Utilities** folder of your **Applications** folder.
- Use the `createinstallmedia` command in Terminal to create the bootable installer. For detailed usage instructions, make sure that the appropriate macOS installer is in your Applications folder, then enter one of the following paths in Terminal:

Path for High Sierra:

```
/Applications/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia
```

Path for Sierra:

```
/Applications/Install\ macOS\ Sierra.app/Contents/Resources/createinstallmedia
```

Path for El Capitan:

```
/Applications/Install\ OS\ X\ El\ Capitan.app/Contents/Resources/createinstallmedia
```

Path for Yosemite:

```
/Applications/Install\ OS\ X\ Yosemite.app/Contents/Resources/createinstallmedia
```

Path for Mavericks:

```
/Applications/Install\ OS\ X\ Mavericks.app/Contents/Resources/createinstallmedia
```

## Examples

This is the basic syntax of the command. Replace `[volumepath]` with the path to your USB flash drive or other volume, and replace `[installerpath]` with the path to the Install OS X app.

## Pre Mojave (< 10.14)

```
createinstallmedia --volume [volumepath] --applicationpath [installerpath]
```

## Post Mojave (> 10.14)

Apple has simplified the `createinstallmedia` command and the `--applicationpath` is deprecated.

```
createinstallmedia --volume [volumepath]
```

The following examples assume that the OS X installer is in your Applications folder and the name of your USB flash drive or other volume is MyVolume:

Example for Sierra:

```
sudo /Applications/Install\ macOS\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume --applicationpath /Applications/Install\ macOS\ Sierra.app
```

> **NOTE:** "`--applicationpath`" is deprecated in macOS 10.14 and greater. Please remove it from your invocation.

## Optional Command

```
--nointeraction &&say Done
```

Example:

```
sudo /Applications/Install\ macOS\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/SierraBootInstall --applicationpath /Applications/Install\ macOS\ Sierra.app --nointeraction &&say Done
```

Source:

- [Create a bootable installer for macOS](https://support.apple.com/en-us/HT201372)
- [How to Create a Bootable macOS Sierra Installer](http://osxdaily.com/2016/09/23/create-boot-macos-sierra-installer/)
- [Create a bootable USB drive for Yosemite the easy way](https://blog.viktorpetersson.com/2014/09/18/create-a-bootable-usb-drive-for-yosemite-the-easy.html)
