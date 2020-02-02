---
layout: post
title:  "Autologin on Kali Lite XFCE4"
date:   2019-11-04 +0700
tags: kalilinux xfce4 login
---
Change this:

`/etc/lightdm/lightdm.conf`

```
[Seat:*]
#autologin-user=root
#autologin-user-timeout=0
```

to this:

```
[Seat:*]
autologin-user=root
autologin-user-timeout=0
```

and change this:

`/etc/pam.d/lightdm-autologin`

```
# Allow access without authentication
auth required pam_succeed_if.so user != root quiet_success
auth required pam_permit.so
```

to this:

```
# Allow access without authentication
#auth required pam_succeed_if.so user != root quiet_success
auth required pam_permit.so
```

Source: [Autologin on Kali Lite after Dist-upgrade on XFCE4](https://forums.kali.org/showthread.php?31854-Autologin-on-Kali-Lite-after-Dist-upgrade-on-XFCE4)
