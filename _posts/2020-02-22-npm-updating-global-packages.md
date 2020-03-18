---
layout: article
title:  "npm: Updating Global Packages"
date:   2020-02-22 15:36:10 +0700
tags: npm node.js update
---

# Updating Global Packages

To update global packages, you can use `npm install -g <package>`:

```
npm install -g expo-cli
```

To find out which packages need to be updated, you can use `npm outdated -g --depth=0`.

To update all global packages, you can use `npm update -g`.

However, for npm versions less than 2.6.1, [this script](https://gist.github.com/othiym23/4ac31155da23962afd0e) is recommended to update all outdated global packages.

Source: [Updating Global Packages](https://npm.github.io/using-pkgs-docs/working-with-packages/updating-global-packages.html)
