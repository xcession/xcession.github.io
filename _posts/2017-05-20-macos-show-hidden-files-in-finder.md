---
layout: article
title:  "macOS: How to Show Hidden Files in Finder"
date:   2017-05-20 18:29:58 +0700
tags: macos finder
---

## Showing Hidden Files in Finder

In the Terminal type:

```
defaults write com.apple.finder AppleShowAllFiles TRUE
killall Finder
```

To set it back (that .DS_Store on the Desktop is hella irritating), execute those same commands, but just switch that `TRUE` to `FALSE`.

Source: [http://lifehacker.com/software/command-line/show-hidden-files-in-finder-188892.php](http://lifehacker.com/software/command-line/show-hidden-files-in-finder-188892.php)
