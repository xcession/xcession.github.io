---
layout: post
title:  "Parallel Tools Fix for Ubuntu"
date:   2019-03-02 02:46 +0700
categories: ubuntu linux debian parallels_desktop macos
---
- Copy the files from the Parallels installation media and drop them in a folder somewhere (eg. `~/parallels_fixed`)
- Go to the kmods directory (`cd ~/parallels_fixed/kmods`) and extract the files (`tar -xzf prl_mod.tar.gz`)
- Remove `prl_mod.tar.gz` file from that directory (`rm prl_mod.tar.gz`)
- Find this file: `~/<your-folder-goes-here>/kmods/prl_fs/SharedFolders/Guest/Linux/prl_fs/prlfs.h`
- Modify the file by going to line 16 and inserting a new line. Add this text: `#include <uapi/linux/mount.h>`
- The file should now look like this. Save and exit.

```
..
#include <linux/fs.h>
#include <uapi/linux/mount.h>
#include <linux/types.h>
..
```

- Go to the `kmods` directory (`cd ~/parallels_fixed/kmods`) and re-zip the files: `tar -zcvf prl_mod.tar.gz . dkms.conf Makefile.kmods` In case you missed it, yes that is a period (`.`) sitting there by itself and necessary.
- Go to the installer directory `cd ~/parallels_fixed/installer`
- `sudo chmod` the script files: `install-cli.sh` (and others) to be executable eg. `sudo chmod 777 *.sh`
- Then run that file with: `sudo ./install-cli.sh -i --verbose`
- Reboot when it's finished.

> **Note:** This also works with other debian based distributions like Kali Linux for example.

Source: [Parallel_Tools_fix_for_Ubuntu_19.04.md](https://gist.github.com/mag911/1a5583a766467d6023584d738cee0d98)
