---
layout: article
title:  "Xcode: Run iOS Emulator Without Starting Xcode"
date:   2017-08-02 20:10:45 +0700
tags: emulator ios macos xcode
---

# Starting iOS Emulator WITHOUT Starting Xcode

Assuming you have Xcode installed in `/Applications`, then you can do this from the command line to start the iPhone Simulator:

```
$ open /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/Applications/iPhone\ Simulator.app
```

You could create a symbolic-link from your Desktop to make this easier:

```
$ ln -s /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/Applications/iPhone\ Simulator.app \~/Desktop
```

As pointed out by @JackHahoney, you could also add an alias to your `~/.bash_profile:`

```
alias simulator='open /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/Applications/iPhone\ Simulator.app'
```

Which would mean you could start the iPhone Simulator from the command line with one easy-to-remember word:

```
$ simulator
``
