---
layout: post
title:  "Backup and Restore Raspberry Pi SD Card on macOS"
date:   2017-02-02 01:15 +0700
categories: raspberry_pi rpi sdcard macos backup restore
---
## Backup FROM the SD card.

- Find the SD card.

    `$ diskutil list`

- Unmount the SD card.

	`$ diskutil unmountDisk /dev/disk#`

- Backup the SD card using dd command.

	`$ sudo dd if=/dev/disk# of=/path/to/image bs=1m`

- Eject the SD card.

	`$ diskutil eject /dev/disk#`

## Restore TO the SD card.

- Find the SD card.

	`$ diskutil list`

- Unmount the SD card.

	`$ diskutil unmountDisk /dev/disk#`

- Restore the backup.

	`$ sudo dd if=/path/to/image of=/dev/disk# bs=1m`

- Eject the SD card.

	`$ diskutil eject /dev/disk#`
