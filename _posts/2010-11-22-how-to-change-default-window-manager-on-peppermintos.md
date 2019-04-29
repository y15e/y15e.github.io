---
layout: post
title: "How to change default window manager on PeppermintOS"
---

The window manager configuration of PeppermintOS is written in **/etc/alternatives/lxdm.conf** file.

The default window manager can be changed by updating

```
session=/usr/bin/startpeppermint
```

to

```
session=/usr/local/bin/enlightenment_start
```
