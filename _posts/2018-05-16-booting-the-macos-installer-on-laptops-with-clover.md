---
layout: article
title:  "Hackintosh: Booting the macOS Installer on Laptop with Clover"
date:   2018-05-16 20:31:19 +0700
tags: clover hackintosh installer laptop
---

# Installing Clover to USB

It is best to use a simple USB2 drive for this purpose. If a USB2 stick doesn't work, try USB3. The ports which will be working without patching (post install process) is hardware dependent.

> **NOTE:** Versions prior to 10.11 fit on an 8GB drive. 10.11 and later can require a larger drive.

Clover and the OS X installer are placed on separate partitions on the USB. There are two options as is relates to USB partitioning:


- Option 1: MBR with a FAT32 partition for Clover and a separate HFS+J partition for the OS X installer.
- Option 2: GPT with a single HFS+J partition for the OS X installer (hidden EFI partition automatically created)

Although you can use Disk Utility to partition your USB, this guide will use 'diskutil' in Terminal. Disk Utility in 10.11 cannot be used for MBR partitioning.

Before you can partition the USB, you must determine what the disk identifier is. With the USB plugged in to the computer, use 'diskutil list':

In Terminal:

```
$ diskutil list
```

In my case, it provides this output:

```
/dev/disk0 (internal, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *500.1 GB   disk0
   1:                        EFI EFI                     209.7 MB   disk0s1
   2:                  Apple_HFS 10.10.x                 80.0 GB    disk0s2
   3:                  Apple_HFS 10.11.gm1               80.0 GB    disk0s3
   4:       Microsoft Basic Data Win10_TP                79.4 GB    disk0s4
   5:                  Apple_HFS 10.10.test              80.0 GB    disk0s5
[B]/dev/disk1 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:                                                   *8.0 GB     disk1[/B]
```

So I can see that the USB is at `/dev/disk1`. Be careful with diskutil as you can lose data without a mechanism for recovery if you repartition the wrong disk.

## Option 1 (MBR, two partitions):

```
# repartition /dev/disk1 MBR, two partitions
# first partition, "CLOVER EFI" FAT32, 200MiB
# second partition, "install_osx", HFS+J, remainder
diskutil partitionDisk /dev/disk1 2 MBR FAT32 "CLOVER EFI" 200Mi HFS+J "install_osx" R
```

The output of the operation looks like this:

```
Started partitioning on disk1
Unmounting disk
Creating the partition map
Waiting for the disks to reappear
Formatting disk1s1 as MS-DOS (FAT32) with name CLOVER EFI
512 bytes per physical sector
/dev/rdisk1s1: 403266 sectors in 403266 FAT32 clusters (512 bytes/cluster)
bps=512 spc=1 res=32 nft=2 mid=0xf8 spt=32 hds=32 hid=2 drv=0x80 bsec=409600 bspf=3151 rdcl=2 infs=1 bkbs=6
Mounting disk
Formatting disk1s2 as Mac OS Extended (Journaled) with name install_osx
Initialized /dev/rdisk1s2 as a 7 GB case-insensitive HFS Plus volume with a 8192k journal
Mounting disk
Finished partitioning on disk1
/dev/disk1 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *8.0 GB     disk1
   1:                 DOS_FAT_32 CLOVER EFI              209.7 MB   disk1s1
   2:                  Apple_HFS install_osx             7.8 GB     disk1s2
```

## Option 2 (GPT, one partition):

```
# repartition /dev/disk1 GPT, one partition
# EFI will be created automatically
# second partition, "install_osx", HFS+J, remainder
diskutil partitionDisk /dev/disk1 1 GPT HFS+J "install_osx" R
```

The output of the operation looks like:

```
Started partitioning on disk1
Unmounting disk
Creating the partition map
Waiting for the disks to reappear
Formatting disk1s2 as Mac OS Extended (Journaled) with name install_osx
Initialized /dev/rdisk1s2 as a 7 GB case-insensitive HFS Plus volume with a 8192k journal
Mounting disk
Finished partitioning on disk1
/dev/disk1 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *8.0 GB     disk1
   1:                        EFI EFI                     209.7 MB   disk1s1
   2:                  Apple_HFS install_osx             7.7 GB     disk1s2
```

> **NOTE:** If you're using Clover legacy, the USB should definitely be MBR.

> **NOTE:** Some BIOS implementations require GPT, some require MBR (many allow both). If you can't get BIOS to recognize your USB for booting, try GPT instead of MBR.

The plist files in this guide require Clover v4359 or newer. For full functionality and best choice, use the latest RehabMan build.

Download the Clover installer. Current builds are available on sourceforge: [http://sourceforge.net/projects/cloverefiboot/](http://sourceforge.net/projects/cloverefiboot/)

Personally, I use my own build/fork of Clover: [https://github.com/RehabMan/Clover](https://github.com/RehabMan/Clover)

After obtaining the Clover installer, first task is to install to the USB "CLOVER EFI" partition.

For Clover UEFI, run the Clover Installer package:

- if using MBR, select the target of the install to "CLOVER EFI" using "Change Install Location"
- if using GPT, select the target of the install to "install_osx" using "Change Install Location"
- select "Customize" (the default is a legacy install -- we need to change it)
- check "Install for UEFI booting only", "Install Clover in the ESP" will automatically select
- check "BGM" from Themes (the config.plist files I provide use this theme)
- check "OsxAptioFixDrv-64" or "AptioMemoryFix.efi" from Drivers64UEFI
- most systems will work without DataHubDxe-64.efi, but some may require it

For Clover legacy, run the Clover Installer package:

- select the target of the install to "CLOVER EFI" using "Change Install Location"
- select "Customize" (we need to change some of the default options)
- "Install for UEFI booting only" will be unchecked
- "Install Clover in the ESP" will be unchecked
- in "Bootloader", check "Install boot0af in MBR" ("Install boot0ss in MBR" for HDD install if dual-boot Windows)
- "CloverEFI" should be checked
- check "BGM" from Themes (the config.plist files I provide use this theme)

Installing to the HDD/SSD after installation is very similar to installing to the USB. Refer back to this section when you get to that stage.

Notes on HDD install:

- you might want "EmuVariableUefi-64.efi", but it would depend on whether native NVRAM works for you (most Skylake hardware has non-functional native NVRAM with OS X/macOS)
- select "Install RC scripts on target volume" and/or "Install all RC scripts on all other boot volumes", but not for USB
- selecting "Install Clover Preference Pane" is optional
- there are also some "Optional RC Scripts" you might want to read about
- if you're installing Clover legacy, check "Install Clover in the ESP"

Note: AptioMemoryFix.efi instead of OsxAptioFix*.efi may allow native NVRAM to work on platforms where it typically does not.

After making your selections you can continue to "Install" the Clover bootloader to your USB.

Finally, we need one EFI driver not included in the Clover installer, **HFSPlus.efi**:

- it can be downloaded from here: [https://github.com/JrCs/CloverGrowerPro/raw/master/Files/HFSPlus/X64/HFSPlus.efi](https://github.com/JrCs/CloverGrowerPro/raw/master/Files/HFSPlus/X64/HFSPlus.efi).
- copy it to `/EFI/Clover/drivers64UEFI`

> **NOTE:** Please, **DO NOT** forget **HFSPlus.efi**. Without it, you won't see any HFS+ partitions, including the HFS+ partition that the OS X installer is on.

Note: For Clover legacy, HFSPlus.efi is built-in (Clover legacy loads no drivers from drivers64UEFI anyway)

If you're installing High Sierra (10.13) to an SSD, keep in mind that the file system will be APFS, which requires apfs.efi in drivers64UEFI. Without **apfs.efi** in drivers64UEFI, Clover will not recognize APFS boot volumes. You can find **apfs.efi** at `/usr/standalone/i386/apfs.efi` inside of "`/Applications/Install macOS High Sierra.app/Contents/SharedSupport/BaseSystem.dmg`".

Now you have the Clover bootloader on the USB, but you still need to configure it correctly.

The resulting drivers64UEFI should look something like this:

```
[driver64UEFI]
|- FSInject-64.efi
|- HFSPlus.efi
|- OsxAptioFixDrv-64.efi
|- OsxFatBinaryDrv-64.efi
```

Note: You may have VboxHfs-64.efi there too. But it doesn't matter. It will be disabled by the config.plist. If you want to use VboxHfs-64.efi you will need to remove the disabler entry for it in config.plist/DisableDrivers.

# Preparing essential kexts

Remove EFI/CLOVER/kexts/10.6, 10.7, 10.8, 10.9, 10.10, leaving just 'Other'

Copy essential kexts to the 'Other' directory (FakeSMC, VoodooPS2Controller). You only need the kexts that allow you to boot and operate the installer. Other kexts that you might use in the final installation can wait.

I always use my own versions of these kexts:

- FakeSMC.kext: [https://github.com/RehabMan/OS-X-FakeSMC-kozlek](https://github.com/RehabMan/OS-X-FakeSMC-kozlek)
- VoodooPS2Controller.kext: [https://github.com/RehabMan/OS-X-Voodoo-PS2-Controller](https://github.com/RehabMan/OS-X-Voodoo-PS2-Controller)
- USBInjectAll.kext may be helpful for reaching the installer (and in post-install... see FAQ)
- USBInjectAll.kext: [https://github.com/RehabMan/OS-X-USB-Inject-All](https://github.com/RehabMan/OS-X-USB-Inject-All)

You may find GenericUSBXHCI.kext useful for non-Intel USB3 (usually only on Sandy Bridge and prior):
GenericUSBXHCI.kext: [https://github.com/RehabMan/OS-X-Generic-USB3](https://github.com/RehabMan/OS-X-Generic-USB3)

For 10.12.5 and HD515/HD520/HD530/HD615/HD620/HD630, you will likely need Lilu.kext and IntelGraphicsFixup.kext:

- Lilu.kext: [https://github.com/vit9696/Lilu](https://github.com/vit9696/Lilu)
- IntelGraphicsFixup.kext: [https://github.com/lvs1974/IntelGraphicsFixup](https://github.com/lvs1974/IntelGraphicsFixup)

With 4k laptop display panel, you will likely need CoreDisplayFixup.kext:
[https://github.com/PMheart/CoreDisplayFixup](https://github.com/PMheart/CoreDisplayFixup)

Note: Please READ the README at each link so you know where pre-built binaries are located. Copy only the kext to Clover/kexts/Other (usually the kext is found in the Release folder inside the ZIP).

Note: GenericUSBXHCI.kext is optional if USB3 ports work with AppleUSBXHCI.kext. GenericUSBXHCI.kext is not compatible with 10.11+. The current version has been modified to do nothing on 10.11+.

Note: The FakeSMC package includes FakeSMC "plugins" (FakeSMC_ACPISensors.kext, FakeSMC_CPUSensors.kext, FakeSMC_LPCSensors.kext, FakeSMC_GPUSensors.kext). You do not need these kexts for installation, although you may wish to try them for getting sensor data to HWMonitor.app after you install. Note: FakeSMC_CPUSensors.kext may have issues on Kaby Lake hardware.

Unlike installing kexts to /System/Library/Extensions, where a kext installer (such as Kext Wizard) must be used, for EFI/Clover/kexts/Other, it is simple copy/paste with Finder.

If your SATA is in RAID mode, you'll need an injector kext. I built one a while back, but it is attached to this post SATA-RAID-unsupported.kext (was SATA-100-unsupported-282a.kext, before that... HPRAIDInjector.kext).

Also, some Skylake SATA controller device-ids are not in the AppleAHCIPort.kext Info.plist (yet). If you have an unsupported SATA controller (8086:a103, 8086:9d03), use SATA-100-series-unsupported.kext. It is also attached to the bottom of this post.

If your main SSD is NVMe, make sure you read important NVMe information in the FAQ:
[http://www.tonymacx86.com/el-capita...faq-read-first-laptop-frequent-questions.html](http://www.tonymacx86.com/el-capita...faq-read-first-laptop-frequent-questions.html)

If you want to have Ethernet (note Ethernet is wired networking, and is not the same as WiFi), you can also install your Ethernet kext.

For example:

- RealtekRTL8111.kext: [https://github.com/RehabMan/OS-X-Realtek-Network](https://github.com/RehabMan/OS-X-Realtek-Network)
- RealtekRTL8100.kext: [http://www.insanelymac.com/forum/topic/296190-driver-for-realteks-rtl810x-fast-ethernet-series/](http://www.insanelymac.com/forum/topic/296190-driver-for-realteks-rtl810x-fast-ethernet-series/)
- AppleIntelE1000e.kext: [http://www.insanelymac.com/forum/topic/205771-appleintele1000ekext-for-108107106105/](http://www.insanelymac.com/forum/topic/205771-appleintele1000ekext-for-108107106105/)
- IntelMausiEthernet.kext: [https://github.com/RehabMan/OS-X-Intel-Network](https://github.com/RehabMan/OS-X-Intel-Network)

A typical EFI/Clover/kexts would look like this:

```
[kexts]
|- [Other]
	|- FakeSMC.kext
	|- IntelMausiEthernet.kext
	|- RealtekRTL8111.kext
	|- VoodooPS2Controller.kext
```

Choosing a config.plist

The Clover installer places a default config.plist at /EFI/Clover/config.plist. It is almost universally wrong and most likely will not work at all for most laptops.

You should choose one that matches your hardware from this repository: [https://github.com/RehabMan/OS-X-Clover-Laptop-Config](https://github.com/RehabMan/OS-X-Clover-Laptop-Config). As you can tell by looking at the listing of files, the configs vary by graphics hardware configuration. If your screen is 1366x768, pick one of those. If your system is mixed (eg. HD3000 on 7-series, or HD4000 on 6-series) be sure to take that into account. If your screen is 1600x900 (or greater) use one of the 1600x900 config files. Haswell graphics are not dependent on screen resolution.

Note: Clover cannot read HTML (config.plist is a plist/xml), so make sure to download from the "Raw" link or download the entire ZIP to get all files: [https://github.com/RehabMan/OS-X-Clover-Laptop-Config/archive/master.zip](https://github.com/RehabMan/OS-X-Clover-Laptop-Config/archive/master.zip)

In any case you may need to change the ig-platform-id that is used at /Graphics/ig-platform-id. But these configurations work most of the time.

Common ig-platform-ids:
0x01660003: HD4000 1366x768
0x01660004: HD4000 1600x900, 1920x1080
0x01660008, 0x01660009: HD4000 1600x900, 1920x1080

0xa260006: HD4400/HD4600/HD5000
Other Haswell ig-platform-id values: 0xa260005, 0xa260000, 0xa160000, 0xa2e0008, 0xa2e000a

Always use a plist editor (such as Xcode or PlistEdit Pro) when making changes to config.plist.

Note: HD4200, HD4400, and HD4600 on 10.10+ needs special patches/injections, thus the separate config_HD4600_4400_4200.plist. If you're installing Mavericks, use the
config_HD5000_5100_5200.plist instead even for HD4200, HD4400 and HD4600. Actually, either one will work, but there is less work arounds (FakeID) required in 10.9.x. Of course, if you ever update beyond 10.9.x, you will need the appropriate changes to FakeID.

Note: HD5600 on 10.11+ needs special patches/injections, thus the separate config_HD5600.plist. If you're installing Yosemite (not recommended with Broadwell), use config_HD5300_5500_6000.plist.

Copy your selected configuration file, and paste it to /EFI/Clover, make sure it is re-named as config.plist. Clover will only load configurations from /EFI/Clover/config.plist.

In case you cannot boot with a valid ig-platform-id (may need to inject EDID, or patch IOKit/CoreDisplay when you have a 4k display, or other problems), use an invalid ig-platform-id (0x12345678) and deal with the graphics issue at post-install.

DVMT-prealloc on Broadwell/Skylake/Kaby Lake

The Broadwell and Skylake graphics kexts provided by Apple require DVMT-prealloc to be set 64mb or larger. Many laptops set it by default to 32mb, which is not large enough and will cause a KP (kernel panic).

There are ways to set it even if your BIOS does not provide the option, but they are somewhat risky. You can find links to these methods in the laptop FAQ.

Since most laptops come with inadequate DVMT-prealloc, all the plists linked by this guide have a patch for 32MB DVMT-prealloc, enabled by default. You can read about how that patch works here: [https://www.tonymacx86.com/threads/guide-alternative-to-the-minstolensize-patch-with-32mb-dvmt-prealloc.221506/](https://www.tonymacx86.com/threads/guide-alternative-to-the-minstolensize-patch-with-32mb-dvmt-prealloc.221506/)

If your laptop has DVMT-prealloc set as required (64MB or 128MB), you should disable or remove the 32MB patch.

Also, once you enable the patch, you still may have panic... It is because Clover cannot patch a kext that loads outside of kernel cache, and these graphics kexts may not be in cache. To work around this problem, use an invalid ig-platform-id (0x12345678). DO NOT use a bogus FakeID, as that will defeat the purpose. Once you are able to boot with the invalid ig-platform-id, rebuild cache, then boot normally with your intended ig-platform-id.

You can rebuild cache in Terminal:

```
sudo touch /System/Library/Extensions && sudo kextcache -u /
```

Or shorthand in 10.11+

```
sudo kextcache -i /
```

Alternately, you can use IntelGraphicsDVMTFixup.kext, which implements the 32MB DVMT-prealloc patch.
It is available here:
[https://github.com/BarbaraPalvin/IntelGraphicsDVMTFixup](https://github.com/BarbaraPalvin/IntelGraphicsDVMTFixup)

Note regarding CPU power management and SSDTs

If you're getting a panic in AppleIntelCPUPowerManagement and/or SMC_ACPI_PlatformPlugin it may be related to your OEM CPU power management related SSDTs.

Some systems may need to drop some of the OEM SSDTs. This happens most frequently with Sandy Bridge systems (but not all). There are two configurations for DropTables in the provided config.plist files. The default is minimal. The alternate is named #DropTables and is a bit more aggressive. Each configuration resides in config.plist/ACPI. You can use the alternate by renaming DropTables->##DropTables and renaming #DropTables->DropTables (in that order). Depending on how the OEM labels the tables, this may or may not work. If you still have issues, set config.plist/ACPI/SSDT/DropOem=true. You will need to set config.plist/ACPI/SSDT/Generate=true (or the individual CStates/PStates=true) to use DropOem=true or the alternate DropTables.

Always use a plist editor (such as Xcode or PlistEdit Pro) to edit config.plist.

Building the OS X installer

There are two ways to copy the OS X installer to USB:
- 'createinstallmedia' method (recommended)
- BaseBinaries clone method (use when 'createinstallmedia' is not available)

createinstallmedia method

This is the same mechanism you would use to create a USB installer for a real Mac.

It is a single line, executed in Terminal:

```
# copy installer image
$ sudo "/Applications/Install macOS High Sierra.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --nointeraction
```

Then change the name to be less unwieldy...

```
# rename
$ sudo diskutil rename "Install macOS High Sierra" install_osx
```

For Sierra:

```
# copy installer image
$ sudo "/Applications/Install macOS Sierra.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --applicationpath "/Applications/Install macOS Sierra.app" --nointeraction

# rename
$ sudo diskutil rename "Install macOS Sierra" install_osx
```

For El Capitan:

```
# copy installer image
$ sudo "/Applications/Install OS X El Capitan.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --applicationpath "/Applications/Install OS X El Capitan.app" --nointeraction

# rename
$ sudo diskutil rename "Install OS X El Capitan" install_osx
```

Yosemite:

```
# copy installer image
$ sudo "/Applications/Install OS X Yosemite.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --applicationpath "/Applications/Install OS X Yosemite.app" --nointeraction

# rename
$ sudo diskutil rename "Install OS X Yosemite" install_osx
```

Mavericks:

```
# copy installer image
$ sudo "/Applications/Install OS X Mavericks.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --applicationpath "/Applications/Install OS X Mavericks.app" --nointeraction

# rename
$ sudo diskutil rename "Install OS X Mavericks" install_osx
```

This method is not available in ML, Lion, SL.

Using 'createinstallmedia' is the only method that results in the creation of a Recovery partition.

BaseBinaries clone method

Note: ATM, BaseBinaries clone method does not work with High Sierra.

You can do the following steps manually via Disk Utility and the Finder, but it is slightly more concise and clear when written in Terminal:

```
# temporary directory
mkdir /tmp/install_esd

# mount InstallESD.dmg in installer package
hdiutil attach "/Applications/Install OS X El Capitan.app/Contents/SharedSupport/InstallESD.dmg" -readonly -mountpoint /tmp/install_esd -nobrowse

# restore it to target
sudo asr restore --source /tmp/install_esd/BaseSystem.dmg  --target /Volumes/install_osx -erase --format HFS+ --noprompt

# rename the target to be less unwieldy
diskutil rename "OS X Base System" install_osx

# remove Packages symlink
rm /Volumes/install_osx/System/Installation/Packages

# copy Packages as folder
cp -a /tmp/install_esd/Packages /Volumes/install_osx/System/Installation

# copy BaseSystem.dmg
cp -a /tmp/install_esd/BaseSystem.dmg /tmp/install_esd/BaseSystem.chunklist /Volumes/install_osx

# unmount InstallESD.dmg
hdiutil detach /tmp/install_esd

# remove temporary directory
rmdir /tmp/install_esd
```

You are now ready to eject your USB device.

## BIOS settings

In order to boot the Clover from the USB, you should visit your BIOS settings:

- "VT-d" (virtualization for directed i/o) should be disabled if possible (the config.plist includes dart=0 in case you can't do this)
- "DEP" (data execution prevention) should be enabled for OS X
- "secure boot " should be disabled
- "legacy boot" optional (recommend enabled, but boot UEFI if you have it)
- "CSM" (compatibility support module) enabled or disabled (varies) (recommend enabled, but boot UEFI)
- "fast boot" (if available) should be disabled.
- "boot from USB" or "boot from external" enabled
- SATA mode (if available) should be AHCI

Note: If you get a "garbled" screen when booting the installer in UEFI mode, enable legacy boot and/or CSM in BIOS (but still boot UEFI). Enabling legacy boot/CSM generally tends to clear that problem.

Arrandale/1st gen Intel HD

First generation Intel HD graphics are not well supported, and require significant post-install patching. See this link for more information: http://www.insanelymac.com/forum/topic/286092-guide-1st-generation-intel-hd-graphics-qeci/

To reach the installer, use a bogus FakeID (Clover Options -> Graphics Injector -> FakeID), such as 0x12345678.

# Booting the Installer

After you create you USB, it is ready to go... Read post #2 for more details on using the USB.

Generally, you will need to use a special button to turn the laptop on or press some special keys to access the boot menu, where you can choose to boot the USB.

Note that you may see it listed twice (depending on setting of legacy boot). Choose the listing that is UEFI or legacy depending on what type of USB you opted for. Of course, if your computer doesn't have UEFI, you'll see no such listing and will boot the device in legacy mode in order to boot Clover.

You can press the spacebar in Clover to select various options. It is a good idea to use this to boot verbose (the config.plist files I provide do not have verbose turned on by default). In verbose mode you have a better idea of the booting process and get better information in the case of a crash.

# Clover Resources

It is a good idea to become familiar with the software you are using and read the documentation.

Clover wiki: http://clover-wiki.zetam.org/Home

Clover instructions thread: http://www.insanelymac.com/forum/topic/282787-clover-v2-instructions/

Clover discussion: http://www.insanelymac.com/forum/topic/284656-clover-general-discussion/

Clover patch/bug reports: http://www.insanelymac.com/forum/topic/306156-clover-bugissue-report-and-patch/

Clover changes: http://www.insanelymac.com/forum/topic/304530-clover-change-explanations/

# Installation and Post Installation

## Using the OS X Installer

Now you have your USB installer, so now you need to use it on the target computer.

Note: It is possible to install when Windows is already installed (UEFI). But it can still be tricky due to the fact that OS X is not well behaved with disks partitioned by other than OS X Disk Utility. See this thread for more information if you plan that route: [http://www.tonymacx86.com/multi-booting/133940-mavericks-windows-8-same-drive-without-erasing.html](http://www.tonymacx86.com/multi-booting/133940-mavericks-windows-8-same-drive-without-erasing.html)

When using Clover, the process of installing OS X is very similar to installing on an actual Mac. This part of the guide will cover the installation process itself.

1. Plug the flashdrive to one of the USB ports. Boot your computer to that USB device. The mechanism varies here, with most computers using one of the F1..F12 keys, Esc key, or (newer computers) have a dedicated power button for boot device selection, BIOS settings, etc. Refer to your user manual if necessary.

2. Clover bootloader screen shows up, select "install_osx". This is the partition on the USB you created earlier. Note: You can press spacebar at this point to change how Clover boots OS X (verbose, without caches, etc). Verbose is a good idea when you're not certain if it is going to work.

3. Press spacebar (or plug in a USB keyboard) if a nagging screen about Mouse/keyboard appears. Install screen will appear, use Disk Utility to partition your drive as GPT, create a Mac OS X Extended (Journaled) partition and install OS X to your formatted partition. If you used the "Unibeast method" or "BaseBinaries clone method", skip to step 7. If you used the 'createinstall media' method, please continue, the installer will extract necessary files to and verify them against the USB. This takes a lot of time at the end, though you only see "a minute remaining". This will end PHASE 1.

4. Restart and again boot to your USB as you did in step 1.

5. Clover bootloader screen shows up. For versions prior to 10.12, select "install_osx" as you did in step #2 (your OS X Installer partition, not your install target partition). Note that macOS Sierra is a bit different in that you will see an "Boot macOS Install from ..." entry in Clover on your target partition at this stage. For 10.12, boot that entry instead of install_osx on the USB.
> Note: For High Sierra 10.13 (or later), you may wish to avoid conversion to APFS. Read here for details: [https://www.tonymacx86.com/threads/guide-avoid-apfs-conversion-on-high-sierra-update-or-fresh-install.232855/](https://www.tonymacx86.com/threads/guide-avoid-apfs-conversion-on-high-sierra-update-or-fresh-install.232855/)

6. Install screen will appear and continue installation. This time, installer will install files to your target partition and create Recovery HD partition. This will end PHASE 2.

7. Restart and again boot to your USB as you did in step 1 and step 4.

8. Clover bootloader screen shows up, select "Boot OS X from YourPartition". "YourPartition" will be named depending on what you chose in Disk Utility in step 3.

9. If everything goes well, you will finish up the installation process and arrive at the OS X desktop.

A note regarding High Sierra and dual-GPU laptops (Nvidia Optimus)

Keep in mind that you will probably need to keep the Nvidia drivers from loading.

Read here for details:
[https://www.tonymacx86.com/threads/fix-window-server-service-only-ran-for-0-seconds-with-dual-gpu.233092/](https://www.tonymacx86.com/threads/fix-window-server-service-only-ran-for-0-seconds-with-dual-gpu.233092/)

## Post Installation

10. At this point, you are ready for "Post Installation", you first step should be to install the Clover bootloader to your HDD. Installing Clover to your HDD is very similar to installing to the USB installer. See post #1 for details.

11. After installing the bootloader, you should take an inventory of things working and not working. Typically, at this point you will have:

- working bootloader via Clover (system should boot relatively quickly from the HDD)
- graphics QE/CI working via Clover's config.plist settings
- PS2 keyboard/trackpad (although perhaps not optimal if you don't have a Synaptics trackpad)
- audio not working
- ethernet not working
- WiFi not working
- brightness controls not working
- certain function keys may not work
- battery status not working
- etc

For each problem there may be a combination of DSDT/SSDT patches required or kexts you need to seek out and install. DPCIManager should be used to get an inventory of the various hardware devices you need drivers/fixes for. Google/search is useful for various issues as are the stickies at the top of this forum. Search within the forum for solutions that may be posted for different laptops but with the same hardware you have. You will be surprised how similar many laptops are.

And guides for specific laptops can offer clues about how to finalize the installation.

Note: The instructions here borrow a bit from nguyenmac's ProBook guide, which is also a useful source of information (but much of it ProBook specific, so filter accordingly): [http://www.tonymacx86.com/hp-probook-yosemite/143675-guide-install-yosemite-hp-laptops-clover-uefi.html](http://www.tonymacx86.com/hp-probook-yosemite/143675-guide-install-yosemite-hp-laptops-clover-uefi.html)

HD4200/HD4600/HD4400 mobile: By using the config.plist for HD4600, you'll have CI, but not QE. HD4400 has QE/CI but there will be other problems in the system (Preview/Safari/etc). You will need to install the two kexts (FakePCIID.kext, FakePCIID_HD4600_HD4400.kext) linked here:

10.11+: [http://www.tonymacx86.com/el-capitan-laptop-support/175797-fix-hd4200-hd4400-hd4600-hd5600-10-11-a.html](http://www.tonymacx86.com/el-capitan-laptop-support/175797-fix-hd4200-hd4400-hd4600-hd5600-10-11-a.html)

10.10: [http://www.tonymacx86.com/yosemite-laptop-support/145427-fix-intel-hd4200-hd4400-hd4600-mobile-yosemite.html](http://www.tonymacx86.com/yosemite-laptop-support/145427-fix-intel-hd4200-hd4400-hd4600-mobile-yosemite.html)

The FAQ covers many typical issues/problems: [http://www.tonymacx86.com/yosemite-laptop-support/164990-faq-read-first-laptop-frequent-questions.html](http://www.tonymacx86.com/yosemite-laptop-support/164990-faq-read-first-laptop-frequent-questions.html)

## Installing Kexts

You should install all kexts you need (including FakeSMC, VoodooPS2Controller, etc) to /Library/Extensions (/L/E) or /System/Library/Extensions (/S/L/E) for 10.10.x and prior using a kext installer or Terminal. Think carefully about "kexts you need". For example, if you needed HPRAIDInjector.kext for a SATA chip locked in RAID mode, you'll need to install it in order to boot (without it, the system would be unable to mount root and would get stuck early in the boot process).

Of course, essential kexts should be installed to EFI/Clover/kexts/Other as they are needed to boot the installer (during updates) or the recovery partition.

It is a mistake to install everything to Clover/kexts. Contrary to popular hackintosh myth, it does not result in a cleaner install (the opposite is true). Many kexts will not work from Clover/kexts, so installing them to /S/L/E where they can be included in kernel cache is the best approach.

People often ask me why I install kexts to /S/L/E (or /L/E on 10.11).

I have many reasons:
- placing them in /S/L/E (or /L/E on 10.11+) and including in kernel cache, makes kextcache do a lot of error checking.
- if you develop kexts, error checking is very important!
- some kexts don't work from Clover/kexts (AppleHDA injector, CodecCommander, BrcmFirmware*)
- the idea behind Clover/kexts is to have a set of *stable* and *minimalistic* kexts that will allow booting of the installer/recovery, not full functionality
- so...the kexts there I tend to not update as often and the full set is not there (less unneeded kexts, less problems)
- placing kexts into kernel cache for day-to-day use is "more native" (as it would be on a real Mac) vs. injection (which is very non-Mac)

IMO, placing kexts in Clover/kexts for injection when not needed is like "flying blind." I don't know about you, but I would not board a plane with a blind pilot (no offense to the blind).

You might be wondering if this will result in duplicate kexts being loaded due to the kexts in EFI/Clover/kexts being injected when they are also installed to the system volume. The answer is no, not generally. With config.plist/SystemParameters/InjectKexts="Detect", kexts in EFI/Clover/kexts are not injected when FakeSMC.kext is in kernel cache. Because FakeSMC.kext is always a "kext you need", you will always install it to the system volume, which will put it in kernel cache. Kernel cache, of course, will not have FakeSMC.kext when booting the installer or recovery, so in these cases the kexts in EFI/Clover/kexts *will* be injected as you would expect.

## Mounting EFI

Eventually, you'll want to make changes to the config.plist, kexts, or other Clover configuration items on the EFI partition. To access the EFI partition, you must mount it manually. Unlike other volumes, it is not mounted automatically.

I wrote a script that I use from Terminal called mount_efi.sh.

You can install/use it as follows...

Download and install mount_efi.sh:

```
# download it
curl --output /tmp/mount_efi.sh https://raw.githubusercontent.com/RehabMan/Lenovo-U430-Touch-DSDT-Patch/master/mount_efi.sh
# copy to /usr/bin
sudo cp /tmp/mount_efi.sh /usr/bin
# allow execute permissions
sudo chmod +x /usr/bin/mount_efi.sh
```

To use it in Terminal:

```
sudo mount_efi.sh
```

Note that in a single disk system with a typical EFI partition labeled 'EFI', you can mount/unmount EFI quite simply with 'diskutil' in Terminal.

To mount EFI:
```
diskutil mount EFI
```
 
To unmount:
```
diskutil unmount EFI
``` 

ForceKextsToLoad

Looking at your config.plist, you will notice an entry in KernelAndKextPatches/ForceKextsToLoad for IONetworkingFamily.kext. This is intended only for installation scenarios and should probably be removed for post-install.

Disabled patches in the config.plist files

There are a number of useful patches in the provided config.plist files. These patches are disabled as some of them are system specific, or specific to a particular version of OS X. You will probably find guides that will mention the same patches.

Instead of entering the patches manually, you can simply enable the patches already in the config.plist. Patches to kexts are based on patching a kext by name. I have modified the name so it does not match by prefixing the name with 'disabled:'. Simply remove the 'disabled:' to match against the real kext and enable the patch. For example, patches for the boot glitch fix against 'IOGraphicsFamily' are default disabled with 'disabled:IOGraphicsFamily'. Change 'disabled:IOGraphicsFamily' to 'IOGraphicsFamily' to enable the patch.

Note: The current plists do not use a modified name, but instead use a new feature in Clover where for each entry, Disabled=true will disable the patch. Change Disabled=false to enable the patch.

There are also some common patches, not specific to graphics architecture, in config_patches.plist. You can use copy/paste to copy these patches, if needed, into your own config.plist.

More information on KextsToPatch at the Clover wiki.

Please read the comment in each patch to know more about its purpose.

Always use a plist editor (such as Xcode or PlistEdit Pro) when making changes to config.plist.

Dual boot Windows UEFI

Dual booting Windows is easy with UEFI (no more boot records!), but there are some caveats.

To dual boot Windows in UEFI mode:
- leave "free space" or use an HFS+J "placeholder" partition on your HDD to install Windows
- DO NOT create any Windows partitions in Disk Utility (doing so will create an MBR/GPT hybrid, which Windows will see as MBR and Windows UEFI requires GPT)
- run the Windows installer in UEFI mode (make sure you boot with the UEFI entry corresponding to the Windows installer USB/DVD)

After installing Windows, you may lose Clover. This is because Windows has set itself as the active UEFI bootloader (a UEFI BIOS setting, often hidden).

To recover Clover, easy way:
- on the EFI partition: rename EFI/Microsoft/Boot/bootmgfw.efi to bootmgfw-orig.efi

After a Windows update, Windows may re-create bootmgfw.efi with updated code. To fix after a Windows update:
- on the EFI partition, remove EFI/Microsoft/Boot/bootmgfw-orig.efi
- rename EFI/Microsoft/Boot/bootmgfw.efi to bootmgfw-orig.efi

You can also use 'efibootmgr' in Linux to add a Clover entry and fix the boot order.
(Linux is free. Ubuntu can be run directly from a USB without installing)

Note: I used Ubuntu. Some have reported problems with efibootmgr in other Linux distros.

For example:

```
# add Clover entry
sudo efibootmgr -c -L "Clover UEFI" -l "\EFI\CLOVER\CLOVERX64.EFI"
```

Most of the time, the new entry will be added to the BootOrder first. But if not, you can change it.

Change the argument to -o based on output from efibootmgr (assumes "Clover UEFI" entry was added as Boot0004):

```
# change order (if needed)
sudo efibootmgr -o 4
```

The advantage of using 'efibootmgr' is that you won't need to rename bootmgfw.efi and Clover won't be lost as a result of Windows updates.

Some laptops have a way to set the UEFI boot entry (or entries) directly in BIOS. Keep in mind that UEFI uses backslash as directory separators, not forward slash.

Windows time vs. OS X time

Windows expects the real time clock to be set to local time. OS X expects UTC. You can change Windows to use UTC by editing RealTimeIsUniversal in the Windows registry.

[http://www.tonymacx86.com/general-help/133719-fix-incorrect-time-windows-osx-dual-boot.html](http://www.tonymacx86.com/general-help/133719-fix-incorrect-time-windows-osx-dual-boot.html)

Find My Mac/Locking

Find My Mac does not work properly. DO NOT lock your hack because it's difficult (or impossible) to unlock again.

If you ignore this advice and lock your hack anyway, this thread may help you: [http://www.tonymacx86.com/hp-probook-yosemite/149208-probook-4440s-asking-6-digit-system-pin.html#post940602](http://www.tonymacx86.com/hp-probook-yosemite/149208-probook-4440s-asking-6-digit-system-pin.html#post940602)

Source: [Booting the OS X installer on LAPTOPS with Clover](https://www.tonymacx86.com/threads/guide-booting-the-os-x-installer-on-laptops-with-clover.148093/)
