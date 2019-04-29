---
layout: post
title: "How to mount USB drive with write access permission"
---

I want to use Songbird to listening music, so I have to mount USB device.

```
sudo mount /dev/sdb1 /mnt/sdb1 -o rw,users,umask=000
```

or if already mounted, then

```
sudo mount /dev/sdb1 /mnt/sdb1 -o remount,rw,users,umask=000
```
