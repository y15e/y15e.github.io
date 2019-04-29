---
layout: post
title: "Disable mouse grab/ungrab on VMware player"
---
Add following lines to **%APPDATA%\VMware\preferences.ini** file.

```
pref.motionGrab = "FALSE"
pref.motionUngrab = "FALSE"
```
