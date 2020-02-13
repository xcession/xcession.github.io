---
layout: article
title:  "macOS: Enable Dock Suck Minimize Effect"
date:   2018-01-31 08:28:20 +0700
tags: macos dock
---

## Enable "Suck" Minimize Effect

- Open Terminal window.
- Enter following command.

```
defaults write com.apple.dock mineffect -string suck
```

- Restart Dock by using following command.

```
killall Dock
```

- Done!

Source: [How to Add the "Suck" Minimize Effect to Your Dock Preferences](https://www.amsys.co.uk/2012/05/how-to-add-the-suck-minimize-effect-to-your-dock-preferences/)
