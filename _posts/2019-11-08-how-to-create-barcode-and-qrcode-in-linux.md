---
layout:	article
title:	"How to Create Barcode in Linux"
date:	2019-11-08 20:34 +0700
categories: linux barcode
---
## Install GNU Barcode

On Debian based distribution:

```
$ sudo apt-get install barcode
```

On Arch Linux:

```
$ sudo pacman -S barcode
```

### To Create a Barcode

Create the barcode by using the following command:

```
$ barcode -b "mycode2792" -o first.ps
```

By default the `barcode` command is output to postscript file (`.ps`), but you can change it to other format such as SVG by using `-S` command option:

```
$ barcode -b "mycode2792" -S -o first.svg
```

Source: [How to Create Bar Code and QR Code in Ubuntu](https://www.linuxhelp.com/how-to-create-bar-code-and-qr-code-in-ubuntu)

