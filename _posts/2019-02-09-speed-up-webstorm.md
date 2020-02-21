---
layout: article
title:  "JetBrains: Speed Up WebStorm"
date:   2019-02-09 22:18:27 +0700
tags: jetbrains webstorm
---

## Speed Up WebStorm

- Go to **Preferences** and do next:
    - **Appearance & Behaviour > System Settings > Updates**: disable auto update
    - **Appearance & Behaviour > System Settings > Usage Statistics**: Uncheck `Allow sending data usage statistics to JetBrains`
    - **Editor > Live Templates**: disable all, leave only what you are really use
    - **Editor > Emmet**: disable all emmets
    - **Editor > Intentions**: I leave only: CSS, Declaration, JavaScript and Language Injection
    - **Plugins**: leave only next (* - can be also disabled in case you don't need them):
        - CoffeeScript *
        - CSS Suport
        - CVS Integration
        - Git Integration
        - HTML Tool
        - IntelliLang
        - JavaScript Debugger *
        - JavaScript Intention Power Pack
        - JavaScript Support
        - NodeJS *
        - Perforce Integration
        - SASS suport *
    - **Project > Directories**: Exclude all what you don't use
    - **Languages & Frameworks > JavaScript > Libraries**: leave only: HTML and HTML5 / EcmaScript 5
    - **Languages & Frameworks > Compass**: disable it
    - **Tools > WebBrowsers**: leave only Chrome

- **Help > Edit Custom VM Options**: Edit and increase usage memory pwd:

```
    -Xms1024m
    -Xmx1536m
    -XX:MaxPermSize=1024m
    -XX:ReservedCodeCacheSize=512m
    -XX:+UseCompressedOops
```

So the main idea is next: disable all in Preferences what you really don't use and increase memory for IDE.


Source: [How to speed up WebStorm](https://stackoverflow.com/questions/29388626/how-to-speed-up-webstorm)
