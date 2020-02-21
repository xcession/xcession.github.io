---
layout: article
title:  "macOS: Create a Bootable Installer for macOS"
date:   2017-09-09 15:45:11 +0700
tags: macos installer usb flashdrive bootable
---

## Create a macOS bootable installer

> You can use an external drive or secondary volume as a startup disk from which to install the Mac operating system.

These advanced steps are intended primarly for system administrators and others who are familiar with the command line. Make sure you use a USB flash drive or other removable media that has at least 12GB of available disk space.

## Download macOS

Find the appropriate download link in the upgrade instructions for each macOS version:

- [macOS Catalina](https://support.apple.com/kb/HT201475), [macOS Mojave](https://support.apple.com/kb/HT210190), and [macOS High Sierra](https://support.apple.com/kb/HT208969) download directly to your Applications folder as an app named Install macOS Catalina, Install macOS Mojave, or Install macOS High Sierra. If the installer opens after downloading, quit it without continuing installation.
 > To get the required installer, download from a Mac that is using [macOS Sierra 10.12.5 or later](https://support.apple.com/kb/HT201260), or El Capitan 10.11.6. Enterprise administrators, please download from Apple, not a locally hosted software-update server.
- [macOS Sierra](https://support.apple.com/kb/HT208202) downloads as a disk image that contains a file named InstallOS.pkg. Open this file and follow the onscreen instructions. It installs an app named Install macOS Sierra into your Applications folder.
- [OS X El Capitan](https://support.apple.com/kb/HT206886) downloads as a disk image that contains a file named InstallMacOSX.pkg. Open this file and follow the onscreen instructions. It installs an app named Install OS X El Capitan into your Applications folder. 

### Use the 'createinstallmedia' command in Terminal

- Connect the USB flash drive or other volume. You could also use a secondary internal partition that has at least 12GB of available disk space for the installation files.
- Open the **Terminal.app**, which is in the **Utilities** folder of your **Applications** folder.
- Use the `createinstallmedia` command in Terminal to create the bootable installer. For detailed usage instructions, make sure that the appropriate macOS installer is in your Applications folder, then enter one of the following paths in Terminal:

#### Post Mojave (> 10.14)

Apple has simplified the `createinstallmedia` command and the `--applicationpath` is deprecated.

```
createinstallmedia --volume [volumepath]
```

**Catalina**:
```
sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume [volumepath]
```

**Mojave**:
```
sudo /Applications/Install\ macOS\ Mojave.app/Contents/Resources/createinstallmedia --volume [volumepath]
```

#### Pre Mojave (< 10.14)

```
createinstallmedia --volume [volumepath] --applicationpath [installerpath]
```

**High Sierra**:
```
sudo /Applications/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia --volume [volumepath] --applicationpath [installerpath]
```

**Sierra**:
```
sudo /Applications/Install\ macOS\ Sierra.app/Contents/Resources/createinstallmedia --volume [volumepath] --applicationpath [installerpath]
```

**El Capitan**:
```
sudo /Applications/Install\ OS\ X\ El\ Capitan.app/Contents/Resources/createinstallmedia --volume [volumepath] --applicationpath [installerpath]
```

**Yosemite**:
```
sudo /Applications/Install\ OS\ X\ Yosemite.app/Contents/Resources/createinstallmedia --volume [volumepath] --applicationpath [installerpath]
```

**Mavericks**:
```
sudo /Applications/Install\ OS\ X\ Mavericks.app/Contents/Resources/createinstallmedia --volume [volumepath] --applicationpath [installerpath]
```

This is the basic syntax of the command. Replace `[volumepath]` with the path to your USB flash drive or other volume, and replace `[installerpath]` with the path to the Install OS X app.

#### Example

The following examples assume that the OS X installer is in your Applications folder and the name of your USB flash drive or other volume is MyVolume:

Example for Sierra:

```
sudo /Applications/Install\ macOS\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume --applicationpath /Applications/Install\ macOS\ Sierra.app
```

> **NOTE:** "`--applicationpath`" is deprecated in macOS 10.14 and greater. Please remove it from your invocation.

#### Optional Command

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

