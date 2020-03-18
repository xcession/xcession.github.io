---
layout: article
title:  "macOS: Customize the About This Mac Section of a Mac"
date:   2017-10-12 16:02:40 +0700
tags: customize macos
---

# Customizing the About This Mac

> ****BACK UP** the original file to a safe location on your computer before modifying it, in case of a mistake or wanting to revert to stock later.

# Changing the System Logo

This section will modify the circular image of your OS version on the main “About This Mac” page. On older OS versions, this used to be an image of your computer hardware.

- Open a Finder window, and navigate to your `/Applications` folder. Find the `/Utilities` folder inside, and inside that, the `System Information.app` application.
- Right-click the application and select **Show Package Contents**.
- Once inside the application, look inside `Contents/Resources`. Find the file entitled **SystemLogo.tiff**.
- **Backup** the original file, and then replace it with the image you want to use. It **must** be renamed to **SystemLogo.tiff**, **SystemLogo.png**, **SystemLogo.jpg**, etc.
- After a logout/login or reboot the new image should appear in place of the pedestrian Sierra logo. For illustrative purposes I chose an image of the most pathetic piece of hardware known to Rick-kind.

For future reference, the full file path for this image is:

```
/Applications/Utilities/System Information.app/Contents/Resources/SystemLogo.tiff
```

To revert, simply replace your backup of the original file, overwriting your edited image.

# Changing the Model Name and Year

This section will change the reported hardware model and production year on the main “About This Mac” page. On a Hackintosh this page will usually report the Model you have selected in your SMBIOS settings, but you might want it to say something different. For example, for best performance on my hack, I have an iMac model set in my SMBIOS. However, the case I made for it is from an old G5, so I want that model to be reported instead in “About This Mac”. If you are on a real Mac this will likely be just, as they apparently say, “for funsies”.

- Open a Finder window and navigate to your **home User** folder (the one containing your Documents, Pictures, Movies, etc.)
- Inside that, open the **Library** folder. If you cannot see it, it may be hidden. You can [find it with our guide](http://www.idownloadblog.com/2015/03/12/library-folder-mac/). Do not confuse it with `/Library` by mistake, it must be `/Users/YOUR_USERNAME/Library`.
- Inside the folder, open **Preferences** and look for the file entitled `com.apple.SystemProfiler.plist`.
- Copy the file, and paste one somewhere as a backup. Then paste **another** copy to your Desktop to edit. Do not try to edit the file in place, it will not work.
- Right-click the copy on your Desktop and open it with your .plist editor of choice.
- In the editor, look through the file for the **CPU Names** entry which describes the current Model and Year of your computer. Mine originally said “iMac 27-inch, Late 2012”.
- Edit the text in that line to report your preferred hardware name and year, or whatever text you like. Save the document and exit.
- Drag the edited file from your Desktop back into the **~/Library/Preferences** folder we got it from to overwrite the original. Authenticate with your user password if required.
- After a reboot the changes should be visible in the “About This Mac” window.

For future reference, the full file path for the document to edit is:

```
/Users/YOUR_USERNAME/Library/Preferences/com.apple.SystemProfiler.plist
```

To revert, simply replace your backup of the original file, overwriting your edited .plist.

# Changing the processor name

This setting may allow you to change the processor name, but I have had mixed results. It worked on my Hackintosh, but not on my MacBook Pro, so your mileage may vary.

- Open a Finder window, navigate to the **System** folder, and then to the Library folder inside. (Not the “Library” folder we visited in the Model name section).
- Inside **Library**, go to **PrivateFrameworks**, and find **AppleSystemInfo.framework**.
- Inside this framework, navigate to `/Versions/A/Resources/`. Then find the folder for your system language. If yours is English, go to **English.lproj**.
- Inside that folder, find the file **AppleSystemInfo.strings**. Copy the file, and paste one somewhere as a backup. Then paste **another** copy to your Desktop to edit. Do not try to edit the file in place, it will not work.
- Right-click the copy on your Desktop and open it with your editor of choice.
- In the editor, look through the file for the **UnknownCPUKind** entry which describes non-standard CPU models. Mine originally said “Unknown”.
- Edit the text in that line to report your preferred CPU model and speed, or whatever text you like. Save the document and exit.

**Hackintosh only, Mac users skip to Step 9.**

- Open up your Clover `config.plist`, and under the **CPU** section set the **Type** to **Unknown**. I used Clover Configurator for this step but it can be done manually too.

- Drag the edited file from your Desktop back into the folder we got it from to overwrite the original. Authenticate with your user password if required.
- After a reboot the changes **should** be visible in the “About This Mac” window.

And there you have it! My under-powered robot’s CPU is now correctly reported. Remember this section may not work for you, especially on a real Mac, as it will probably not default to the “Unknown CPU” field. Setting the CPU type to “Unknown” in Clover on a Hackintosh forces it to use the field, and therefore work.

For future reference, the full file path for the document to edit is:

```
/System/Library/PrivateFrameworks/AppleSystemInfo.framework/Versions
/A/Resources/YOUR_SYSTEM_LANGUAGE.lproj/AppleSystemInfo.strings
```

To revert, simply replace your backup of the original file, overwriting your edited .strings file.

# Changing the Displays image

This edit is one of the most useful, as many people use external displays, and they come from many third-parties. Consequently, a generic icon is used by Apple in the “Displays” section of “About This Mac”, and in the “Displays” section of “System Preferences”. Many people will wish to change this to an image of their specific external display model.

- Open a Finder window, and navigate to the **System** folder. From there, open **Library**, then **CoreServices**, and locate the file **CoreTypes.bundle**.
- Right-click **CoreTypes.bundle** and select **Show Package Contents**. From there, go to `/Contents/Resources`, and find the file called **public.generic-lcd.icns**.
- Make a backup of this file somewhere safe, and then place an image of your own display, or whatever image you like, into that folder. It will replace the generic display image. Make sure the file you place there is called **public.generic-lcd.icns**. The file must be in .icns format. I use Image2Icon for this; it is [available on the App Store for free](https://geo.itunes.apple.com/us/app/image2icon-make-your-own-icons/id992115977?mt=12&at=11l4L8&ct=SP).
- After a logout/login or reboot, your changes should be visible.

For future reference, the full file path for the document to edit is:

```
/System/Library/CoreServices/CoreTypes.bundle/Contents/Resources/public.generic-lcd.icns
```

To revert, simply replace your backup of the original file, overwriting your edited .icns file.

Source: [How to customize the “About This Mac” section of a Mac](http://www.idownloadblog.com/2017/01/13/how-to-modify-about-this-mac-hackintosh/)
