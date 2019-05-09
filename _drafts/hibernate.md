---
layout: post
title: "Enable hibernation"
---




## Create a swap file

$
$ fallocate -l 2.5G /swapfile
$ chmod 600 /swapfile
$ mkdwap /swapfile

## didn't work

https://wiki.archlinux.org/index.php/Swap#Automated

$ sudo pacman -S systemd-swap

$ vi /etc/systemd/swap.conf
swapfc_enabled=1
