---
layout: post
title:  "How to Update Pi-Hole"
date:   2019-03-02 02:46 +0700
categories: raspberry_pi rpi pihole update
---
We cannot update Pi-hole from the Web interface as we need to restart the server, which would interrupt the update process.

Run the following command on your Pi-hole:

```
# pihole -up
```

You will need to SSH into your machine or access it directly via a keyboard and monitor. Typically, Pi-hole is running as a headless server so SSH is the preferred choice to run the command.

Source: [How do I update Pi-hole?](https://discourse.pi-hole.net/t/how-do-i-update-pi-hole/249)
