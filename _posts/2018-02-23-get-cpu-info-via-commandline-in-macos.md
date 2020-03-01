---
layout: article
title:  "macOS: Get CPU Info via Command Line in macOS"
date:   2018-02-23 20:19:44 +0700
tags: commandline cpu macos terminal
---

## Getting CPU Info from Command Line

- Launch **Terminal**.
- Enter following `sysctl` command.

```
$ sysctl -n machdep.cpu.brand_string
```

The example output may look like any of the following:

```
$ sysctl -n machdep.cpu.brand_string
Intel(R) Core(TM) i5-5257U CPU @ 2.70GHz
```

This is basically in the following format: Chip Brand – Processor Type and Chip Model – CPU Speed

> Intel(R) Core(TM)2 Duo CPU E8600 @ 2.40GHz

## How to Get CPU Processor Details of Mac via Terminal with system_profiler

On the other hand, if you don’t want the model number and simply want processor name, speed, and the number of processors, you can use grep with system_profiler. Still in the Terminal, enter the following command string:

```
$ system_profiler | grep Processor
```

```
Processor Name: Intel Core 2 Duo
Processor Speed: 2.4 GHz
Number of Processors: 1
```

Source: [Get CPU Info via Command Line in Mac OS X](http://osxdaily.com/2011/07/15/get-cpu-info-via-command-line-in-mac-os-x/)
