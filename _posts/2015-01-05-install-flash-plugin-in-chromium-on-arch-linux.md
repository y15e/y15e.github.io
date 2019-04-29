---
layout: post
title: "Install Flash plugin in Chromium on Arch Linux"
---

**flashplugin** package can't be used for Chromium browser on Arch Linux. Use [chromium-pepper-flash](https://aur.archlinux.org/packages/chromium-pepper-flash/) from AUR instead.

```
$ wget https://aur.archlinux.org/packages/ch/chromium-pepper-flash/chromium-pepper-flash.tar.gz
$ tar zvxf chromium-pepper-flash.tar.gz
$ cd chromium-pepper-flash
$ makepkg
$ sudo pacman -U chromium-pepper-flash-1\:16.0.0.235-3-i686.pkg.tar.xz
$ chromium &
```
