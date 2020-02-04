---
layout: article
title:  "React Native: Setting Up the React Native Development Environment on Windows"
date:   2019-11-08 02:49 +0700
tags: react-native windows chocolatey nodejs
---

## Setting Up on Windows

### Install Chocolatey

Windows doesn't really come with its own package manager that we can use to install the needed tools. So the first thing we'll do is install one called [Chocolatey](https://chocolatey.org/).

#### Requirements

- Windows 7+ / Windows Server 2003+
- PowerShell v2+
- .NET Framework 4+ (the installation will attempt to install .NET 4.0 if you do not ave it install)

#### Chocolatey Install

- Ensure that you are using an [administrative shell](http://www.howtogeek.com/194041/how-to-open-the-command-prompt-as-administrator-in-windows-8.1/)
- Install with `powershell.exe` you must ensure [Get-ExecutionPolicy](https://go.microsoft.com/fwlink/?LinkID=135170) is not Restricted.
	- Run `Get-ExecutaionPolicy`. If it returns `Restricted`, then run `Set-ExecutionPolicy AllSigned` or `Set-ExecutionPolicy Bypass -Scope Process`.
- Now run the following command:

```
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

- Wait a few seconds for the command to complete.
- If you don't see any errors, you are ready to use Chocolatey!
- Type `choco` or `choco -?` now.

### Install Python

Python comes with the command line tools required by React Native:

```
choco install -y python 2
```

### Install JDK

The JDK allows your computer to understand and run Java code. Be sure to install JDK version 8 as that's the one required by React Native:

```
choco install jdk8
```

### Install NVM

Node has an [installer for Windows](https://nodejs.org/en/download/). It's better to use NVM for Windows, as that will enable you to install multiple versions of Node so that you can test new versions, or use a different version depending on the project you're currently working on. For that, you can use NVM for Windows. Download [nvm-setup.zip](https://github.com/coreybutler/nvm-windows/releases), extract it and execute `nvm-setup.exe` to install it.

### Install Watchman

Watchman optimizes the compilation time of your React Native app. it's an optional install if you're net working on a large project. You can find the [install instructions on their website](https://facebook.github.io/watchman/docs/install.html#download-for-windows-beta).

### Update the Environment Variables

This is the final step in setting up React Native on Windows. This is where we update the environment variables so the operating system is aware of all the tools required by React Native. Follow these steps right before you install the React Native CLI.

- Go to **Control Panel > System and Security > System**. Once there, click the **Advanced system settings** menu on the left.
- That will open the system properties window. Click on the **Environment Variables** button.
- Under the **User variables** section, highlight the **Path** variable and click the **edit** button.
- On the edit screen,  click the **New** button and enter the path to the Android SDK and platform tools. For example `C:\users\myUsername\AppData\Local\Android\SDK` and `C:\users\myUsername\AppData\Local\Android\Sdk\platform-tools`. Note that this is also where you add the path to the JDK if it isn't already added.

Source:
- [Setting Up the React Native Development Environment](https://www.sitepoint.com/getting-started-with-react-native/)
- [Installing Chocolatey](https://chocolatey.org/install#install-step1)
