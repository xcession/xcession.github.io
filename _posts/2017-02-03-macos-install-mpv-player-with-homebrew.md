---
layout: article
title:  "macOS: Install MPV Player with Homebrew"
date:   2017-02-03 17:24 +0700
tags: macos brew.sh homebrew mpv
---

## Installation

- Install **Xcode** from AppStore.
- Install **Command Line Tools** from `Xcode > Preferences > Downloads`.
- Install Homebrew by running this command in Terminal:

	``$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"``

- Install some other needed stuff:

	``$ sudo easy_install docutils``

- Build mpv and the needed dependencies using Homebrew:

	``$ export LC_ALL=en_US.UTF-8 ; export LANG=en_US.UTF-8``

	``$ brew tap mpv-player/mpv``

	``$ brew install --HEAD --with-bundle --with-bluray-support --with-libdvdread --with-little-cms2 --with-lua --with-bundle mpv``

- If you want to have an .app-bundle in `~/Applications`:

	``$ brew linkapps mpv``

- **Done!**

## Configuration

To make your own configuration, create the folders `~/.config/mpv` and create the file `mpv.conf` in there. Paste the the options you want to change in that file (see mpv’s documentation for all possible options).

If you have sufficient GPU power, it is recommended to use the opengl-hq video-output (requires Intel HD4000 or better). To use this add this line to your config:

	vo=opengl-hq:icc-profile-auto

## Notes

- Remember to keep everything up-to-date using `brew update`. Since mpv is on –HEAD, `brew update` won’t work for it. You need to uninstall and reinstall (`brew rm mpv && brew install --HEAD --with-bundle --with-bluray-support --with-libdvdread --with-little-cms2 --with-lua --with-bundle mpv`), as it’s a HEAD only formula homebrew is not smart enough to figure out the version it built.
- Having MacPorts or Fink installed may break brew. See `brew doctor` if you run into problems.
- If you have problems, join the `#mpv` channel on freenode or open an issue on the [Github page]. Please use the comments here only for problems related to CGi releases.

Source: [https://coalgirls.wakku.to/faq/playback/compiling-mpv-on-mac-os-x](https://coalgirls.wakku.to/faq/playback/compiling-mpv-on-mac-os-x)
