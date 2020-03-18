---
layout: article
title:  "Android: Setting Up Android Studio"
date:   2020-03-07 18:19:03 +0700
tags: android android_studio emulator sdk
---

Updated: 2020-03-18 20:38
{:.info}

# Set Up Android Studio's Tools

- Install Android Studio 3.0+
- Go to **Preferences -> Appearance & Behavior -> Android SDK**. Click on the **SDK Tools** tab and make sure you have at least one version of the **Android SDK Build-Tools** installed.
- Copy or remember the path listed in the box that says **Android SDK Location**.
- If you are on macOS or Linux, add the Android SDK location to your PATH. `~/.bash_profile` or `~/.bash.rc` if you're using BASH or `~/.zshrc` if you're using ZSH.
```
export ANDROID_SDK_ROOT="$HOME/Library/Android/sdk"
export $PATH="$PATH:$ANDROID_SDK_ROOT/emulator"
export $PATH="$PATH:$ANDROID_SDK_ROOT/tools"
export $PATH="$PATH:$ANDROID_SDK_ROOT/tools/bin"
export $PATH="$PATH:$ANDROID_SDK_ROOT/platform-tools"
```
- Make sure you can run `adb` from your terminal.

# Set Up a Virtual Device

- From the Android Studio main screen, go to **Configure -> AVD Manager**.
- Press the **+ Create Virtial Device** button.
- Choose the type of hardware you'd like to emulate. We recommend testing against a variety of devices, but if you're unsure where to start, the newest device in the Pixel ine could be a good choice.
- Select an OS version to load on the emulator (probably one of the system images in the "Recommended" tab), and download the image.
- Change any other settings you'd like, and press "Finish" to create the virtual device. You can now run this device anytime by pressing the Play button in the AVD Manager window.

# Multiple adb versions

Having multiple `adb` versions on your system can result in the error `adb server version (xx) doesn't match this client (xx); killing...`

This is becuase the adb version on your system is different from the adb version on the android sdk platform-tools.

- Open the terminal and check the `adb` version on the syetem:
```
$ adb version
```
- And from the Android SDK platform-tool directory:
```
$ cd ~/Library/Android/sdk/platform-tools
$ ./adb version
```

Source: [Android Studio Emulator](https://docs.expo.io/versions/latest/workflow/android-studio-emulator/)
