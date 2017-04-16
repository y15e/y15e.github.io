---
layout: post
title: "How to change default window manager on PeppermintOS"
---

The default window manager configuration is written in /etc/alternatives/lxdm.conf file.

You can change default window manager by changing

```
session=/usr/bin/startpeppermint
```

to

```
session=/usr/local/bin/enlightenment_start
```

Of course, above is example of my case.
