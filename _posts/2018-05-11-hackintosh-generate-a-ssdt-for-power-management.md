---
layout: article
title:  "Hackintosh: Generate a SSDT for Power Management"
date:   2018-05-11 01:00:57 +0700
tags: hackintosh ssdt powermanagement
---

## Generate a SSDT for Power Management

- Configure system with appropriate SMBIOS for your CPU using Clover Configurator

- Open Terminal and download Piker Alpha's `ssdtPRGen.sh`

```
$ curl -o ~/ssdtPRGen.sh https://raw.githubusercontent.com/Piker-Alpha/ssdtPRGen.sh/master/ssdtPRGen.sh
```
- That will download `ssdtPRGen.sh` to your user directory. The next step is to change the file mode (+x) with:

```
$ chmod +x ~/ssdtPRGen.sh
```

- For default SSDT generation, type:

```
$ sudo ~/ssdtPRGen.sh
```

- Type `n`, `n`

- Open Finder and in menubar choose **Go > Go to Folder**...

- Type `~/Library/ssdtPRGen/`

- Mount EFI using EFI Mounter or Clover Configurator.

- Copy `SSDT.aml` to `/Volumes/EFI/EFI/CLOVER/ACPI/patched/`

> NOTE: The Power Management SSDT should always be SSDT.aml. If you have an SSDT.aml there already, rename it SSDT-1.aml, etc...

- Reboot

## How to Test Power Management

- Download and compile `AppleIntelInfo.kext` using Xcode. Or download here: [View attachment AppleIntelInfo.kext.zip](https://www.tonymacx86.com/attachments/appleintelinfo-kext-zip.160106/).

- Drag `AppleIntelInfo.kext` to desktop

- Open Terminal and type:

```
$ sudo -s
# chown -R 0:0 ~/Desktop/AppleIntelInfo.kext
# chmod -R 755 ~/Desktop/AppleIntelInfo.kext
# kextload ~/Desktop/AppleIntelInfo.kext
# cat /tmp/AppleIntelInfo.dat
```

- The amount of power states will then show in the Terminal window.

Source: [Quick Guide to Generate a SSDT for CPU Power Management](https://www.tonymacx86.com/threads/quick-guide-to-generate-a-ssdt-for-cpu-power-management.177456/)
