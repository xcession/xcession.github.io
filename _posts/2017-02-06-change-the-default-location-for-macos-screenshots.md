---
layout: article
title:  "macOS: Change the Default Location for macOS Screenshots"
date:   2017-02-06 16:14:41 +0700
tags: macos screenshot
---

## Changing the Default Screenshots Save Location

- Create a new folder using Finder (eg. Desktop/Screenshots).
- Go to **Applications > Utilities > Terminal**.
- Type: `defaults write com.apple.screencapture location` then drag the newly created folder to the Terminal screen (and it will insert the file path of the folder for you). Or enter the file location manually if you know what it is (carefully check your spelling and location).

```
defaults write com.apple.screencapture location/Users/USERNAME/Desktop/Screenshots
```

- Type: `killall SystemUIServer`
- All done!

Source: [How To Change The Default Location For macOS Screenshots](https://simonemccallum.com/2013/08/11/how-to-change-the-default-location-for-your-mac-os-x-screenshots/)
