---
layout: article
title:  "Hackintosh: APFS.efi Location"
date:   2019-02-03 18:02:44 +0700
tags: macos hackintosh apfs apfs.efi clover
---

# Locating APFS.efi

To find the current version of `apfs.efi`:

1. Boot into macOS High Sierra
2. Choose **Finder > Go > Go To Folder**
3. Navigate to `/usr/standalone/i386/`
4. Copy `apfs.efi` to `/Volumes/EFI/EFI/CLOVER/drivers64UEFI/`

Source: [How to Update + Current and Past apfs.efi Downloads](https://www.tonymacx86.com/threads/how-to-update-current-and-past-apfs-efi-downloads.236103/)
