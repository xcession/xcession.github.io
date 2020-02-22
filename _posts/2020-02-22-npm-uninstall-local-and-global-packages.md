---
layout: article
title:  "npm: Uninstall Local and Global Packages"
date:   2020-02-22 20:01:18 +0700
tags: node.js npm uninstall
---

## Uninstalling Local Packages

You can remove a package from you node_modules directory using `npm uninstall <package>`:

```
npm uninstall lodash
```

To remove it from the dependencies in `package.json`, you will need to use the save flag:

```
npm uninstall --save lodash
```

## Uninstalling Global Packages

Global packages can be uninstalled with `npm uninstall -g <package>`:

```
npm uninstall -g jshint
```

Source: [Uninstalling Local and Global Packages](https://npm.github.io/using-pkgs-docs/working-with-packages/uninstalling.html)
