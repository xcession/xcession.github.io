---
layout: post
title:  "Fix Permissions on Globally Installing `npm` Packages on Linux"
date:   2019-11-07 18:52:12 +0700
tags: npm node.js linux
---
The difference in `npm` packages that are installed **globally and locally** is that you will setup a package like a program available by a CLI (Command Line Interface), This require permissions to write in some directories that the `npm` normally don't has.

When you try install some globally package (using the `-g`):

```
$ npm install -g [package]
```

You can face error and warning like this:

```
npm WARN checkPermissions Missing write access to /usr/lib/node_modules
npm ERR! path /usr/lib/node_modules
npm ERR! code EACCES
npm ERR! errno -13
npm ERR! syscall access
npm ERR! Error: EACCES: permission denied, access '/usr/lib/node_modules'
npm ERR!  { [Error: EACCES: permission denied, access '/usr/lib/node_modules']
npm ERR!   stack:
npm ERR!    'Error: EACCES: permission denied, access \'/usr/lib/node_modules\'',
npm ERR!   errno: -13,
npm ERR!   code: 'EACCES',
npm ERR!   syscall: 'access',
npm ERR!   path: '/usr/lib/node_modules' }
npm ERR! 
npm ERR! The operation was rejected by your operating system.
npm ERR! It is likely you do not have the permissions to access this file as the current user
npm ERR! 
npm ERR! If you believe this might be a permissions issue, please double-check the
npm ERR! permissions of the file and its containing directories, or try running
npm ERR! the command again as root/Administrator (though this is not recommended).

npm ERR! A complete log of this run can be found in:
```

This is a `EACESS` error that can be fix by creating a directory for global installations, setting `npm` to config the directory and add the `npm-global/bin` to the path of OS (Operating System).

```
$ mkdir ~/.npm-global
$ npm config set prefix '~/.npm-global'
$ export PATH=~/.npm-global/bin:$PATH ### Add this to the end of the file `~/.profile`
$ source ~/.profile`
```

This can be found in: [https://docs.npmjs.com/getting-started/fixing-npm-permissions](https://docs.npmjs.com/getting-started/fixing-npm-permissions)

> **Don't use `sudo`** to install packages globally, this is unsafe choice because `npm` install can run arbitary scripts, you can get more `EACESS` errors later, locally you are creating a directory that only can be managed with `sudo` permissions, don't make this.

Source: [How to fix permissions on globally installing npm packages on linux](https://danillolima.com/npm/how-to-fix-permissions-on-globally-installing-npm-packages-on-linux/)
