---
layout: article
title:  "Linux: Create Desktop Shortcut or Launcher"
date:   2019-05-27 13:13:22 +0700
tags: linux shortcut
---

## Creating Desktop Shortcut or Launcher

Users start programs on Linux with “launchers”. These files contain specific instructions for how the Linux operating system should run the program and how the icon should look, among other things. On Linux, if you want to create application menu shortcuts, you’ll find that it’s a bit more difficult, compared to Mac or Windows, as users can’t just right-click on a program and select the “create shortcut” option. Instead, if you’d like to create application menu shortcuts on the Linux desktop, it’s an involved process that takes a bit of know-how.

A desktop shortcut is represented by a corresponding `.desktop` file which contains meta information of a given app (e.g., name of the app, launch command, location of icon file, etc.). Desktop shortcut files are placed in `/usr/share/applications` or `~/.local/share/applications`. The former directory stores desktop shortcuts that are available for every user, while the latter folder contains shortcuts created for a particular user only.

## Application Menu Shortcuts – Terminal

To manually create a desktop shortcut for a particular program or command, you can create a `.desktop` file using any text editor, and place it in either `/usr/share/applications` or `~/.local/share/applications`. A typical .desktop file looks like the following.

```
[Desktop Entry]
Encoding=UTF-8
Version=1.0                                     # version of an app.
Name[en_US]=yEd                                 # name of an app.
GenericName=GUI Port Scanner                    # longer name of an app.
Exec=java -jar /opt/yed-3.11.1/yed.jar          # command used to launch an app.
Terminal=false                                  # whether an app requires to be run in a terminal.
Icon[en_US]=/opt/yed-3.11.1/icons/yicon32.png   # location of icon file.
Type=Application                                # type.
Categories=Application;Network;Security;        # categories in which this app should be listed.
Comment[en_US]=yEd Graph Editor                 # comment which appears as a tooltip.
```

The first step to creating a new application shortcut in Linux is to create an empty Desktop file. In the terminal, use the `touch` command to create a new shortcut.

```
$ touch ~/Desktop/example.desktop
$ chmod +x ~/Desktop/example.desktop
$ echo '[Desktop Entry]' >> ~/Desktop/example.desktop
```

The new shortcut icon is on the desktop, but it has no program instructions. Let’s fix this by editing the new file in the Nano text editor.

```
nano ~/Desktop/example.desktop
```

The first line for any application shortcut is “Name”. This line will give the application shortcut its name in the menus. In Nano text editor, give your shortcut a name.

```
Name=Example Shortcut
```

Following “Name,” the next line in the shortcut to add is “Comment.” This line is optional but very useful as it allows the menu to display some information about the shortcut.

```
Comment=This is an example launcher
```

With “Name” and “Comment” out of the way, we can get to the real meat of the launcher. In the Nano text editor, add the “Exec” line.

The “Exec” line tells your Linux OS where the program is, and how it should start.

```
Exec=command arguments
```

Exec is very versatile and can launch Python, Bash, and just about anything else you can think of. For example, to run a shell or bash script via the shortcut, do:

```
Exec= sh /path/to/sh/script.sh
```

Alternatively, set your app shortcut to run a Python program with:

```
Exec=python /path/to/python/app
```

Once the “Exec” line is set to your liking, add the “Type” line.

```
Type=Application
```

Need to set your custom shortcut up with an icon? Use the “Icon” line.

```
Icon=/path/to/custom/icon
```

Now that Name, Comment, Exec, and Icon are set, it’s safe to save the custom shortcut. Using the `Ctrl + O` keyboard combination, save the app shortcut. Then, exit Nano with `Ctrl + X`.

Install your custom app shortcut system-wide with:

```
sudo mv ~/Desktop/example.desktop /usr/share/applications
```

## Application Menu Shortcuts – Alacarte

There are many menu editors on Linux. For the most part, they all work similarly and do the same thing. For best results, we recommend using the Alacarte app. It’s easy to use, works on everything and can be installed on even the most obscure Linux distributions (due to it’s relationship to the Gnome project).

### Ubuntu

```
$ sudo apt install alacarte
```

### Debian

```
$ sudo apt-get install alacarte
```

### Arch Linux

```
$ sudo pacman -S alacarte
```

### Fedora

```
$ sudo dnf install alacarte -y
```

### OpenSUSE

```
$ sudo zypper install alacarte
```

### Generic Linux

Not able to find the Alacarte menu editor app on your Linux distribution? [Visit the souce code site](https://gitlab.gnome.org/GNOME/alacarte/) and build it yourself!

Source:
- [Create Desktop Shortcut or Launcher on Linux](http://xmodulo.com/create-desktop-shortcut-launcher-linux.html)
- [How To Create Application Menu Shortcuts On Linux](https://www.addictivetips.com/ubuntu-linux-tips/create-application-menu-shortcuts-linux/)
