---
layout: article
title:  "Fixing FileZilla Window Position on macOS"
date:   2017-08-02 20:08:49 +0700
tags: filezilla macos window
---

## Fixing FileZilla Window Position

Somehow FileZilla window stuck under the macOS menubar.

- Shutting down Filezilla

- Editing `/Users/username/.config/filezilla/filezilla.xml`

Searching for this line:

```
Original: <Setting name="Window position and size">0 0 -56 1504 1126 </Setting>
```

Changing it to:

```
New: <Setting name="Window position and size">10 10 -56 1504 1126 </Setting>
```

- When I opened it back up, it's fixed. :)
