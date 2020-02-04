---
layout: article
title:  "VirtualBox: Storage Disk Image Types"
date:   2019-05-09 21:02 +0700
tags: virtualbox vbox storage diskimage
---

## Supported Disk Image

### Full Support

- VDI
- VMDK
- VHD

### Partial Support

- HDD (Parallels version 2 only)

### [Undocumented](https://www.virtualbox.org/svn/vbox/trunk/src/VBox/Storage/) Support

- QCOW
- QED

## Dynamic Sizing

**VDI**, **VMDK** and **VHD** all support dynamically allocated storage. **VMDK** has an additional capability of splitting the storage file into files less than 2GB each, which is useful if your file system has a small size limit.

**HDD**, **QCOW** and **QED** have to be dynamically allocated if created in VirtualBox.

## Snapshots

VirtualBox supports snapshotting of **all six formats**.

## Moving VM Between OSes or Another Virtualization Software

**VDI** is the native format of VirtualBox. Other virtualization software generally don't support VDI, but it's pretty easy to convert from VDI to another format, especially with [https://linux.die.net/man/1/qemu-img](`qemu-img convert`).

**VMDK** is developed by and for VMWare, but VirtualBox and QEMU (another common virtualization software) also support it.

**VHD** is the native format of Microsoft Virtual PC. Windows Server 2012 introduced **VHDX** as the successor to VHD, but VirtualBox does not support VHDX.

**HDD** is a format for Parallels Desktop. Parallels specializes in virtualization for macOS.
But VirtualBox only supports an old version of the HDD format (version2).

**QCOW** is the old original version of the QCOW format. It has been superseded by **QCOW2**, which VirtualBox does not support.

**QED** was an abandoned enhancement of QCOW2. [QEMU advises against using QED](https://wiki.qemu.org/Features/QED)

Source: [What disk image should I use with VirtualBox?](https://superuser.com/questions/360517/what-disk-image-should-i-use-with-virtualbox-vdi-vmdk-vhd-or-hdd)