---
layout: article
title:  "macOS: Restore, Clone or Backup Homebrew Setup"
date:   2019-03-20 18:46:31 +0700
tags: macos backup restore homebrew brew.sh
---

## Brewfiles

This is where the magic happens. If you ever used `npm`, `bower` or another package-/assetsmanager you might be using dependency files that list a number of packages or assets that are to be installed. `Brewfiles` do about the same but then for your Homebrew configuration.

Let’s get started quickly! Install the Homebrew tap:

```bash
$ brew tap Homebrew/bundle
```

### Dumping all of your Homebrew packages at once

Run the following command to create a text file named `Brewfile` with all Homebrew packaged installed on your system:

```bash
$ brew bundle dump
```

This creates a file with a lot of entries:

```
tap 'caskroom/cask'
tap 'homebrew/bundle'
tap 'homebrew/core'
tap 'homebrew/dupes'
tap 'homebrew/php'
tap 'homebrew/services'
tap 'homebrew/versions'
brew 'android-platform-tools'
brew 'autoconf'
brew 'boost'
brew 'readline'
brew 'calc'
brew 'cscope'
...
```

Keep this file safe in your cloud filestorage like Dropbox or e-mail.

```bash
$ mv Brewfile ~/Dropbox
```

### Restore your configuration

Change your working directory to the folder containing the Brewfile. Then, to install/restore all items in the file, run:

```bash
$ cd ~/Dropbox
$ brew bundle
```

Voilá! Homebrew starts reinstalling all packages.

### Creating a custom Brewfile

The Brewfile syntax is easy. Each line is a command that gets executed. First, create an empty Brewfile:

```bash
$ touch Brewfile
```

Then – as an example – add a tap, a two brew packages and a cask respectively:

```
tap 'homebrew/php'
brew 'homebrew/php/php71', args: ['with-imap']
brew 'shpotify'
cask 'spotify'
```

Isn’t it nice?

Source: [Restore, Clone or Backup your Homebrew Setup](https://tomlankhorst.nl/brew-bundle-restore-backup/)
