---
layout: post
title: "Use Canon LBP 3100 Printer from Arch Linux"
---

(1) Install CUPS (Common Unix Printing System) via pacman.

```
$ sudo pacman -S cups
```

(2) Start CUPS daemon.

```
$ sudo systemctl start org.cups.cupsd.service
```

(3) Open web interface url [http://localhost:631/](http://localhost:631/) by using browser.

You will see following page.
![CUPS web interface](/assets/img/cups-web-interface.jpg)


(4)

```
$ sudo /usr/sbin/groupadd printadmin
$ sudo /usr/sbin/gpasswd -a myusername printadmin
$ sudo /usr/sbin/gpasswd -a myusername lp
```

**/etc/cups/cups-files.conf**

```
SystemGroup sys root **printadmin**
```

```
$ sudo systemctl restart org.cups.cupsd.service
```

(5)

```

```
Download a linux driver from [Canon's web site](http://cweb.canon.jp/drv-upd/lasershot/linux/captlinuxx64.html)

$ sudo pacman -S rpmextract
$ cd ~/Downloads
$ tar zxvf linux-capt-printerdriver64-260.tar.gz
$ cd ./linux-capt-printerdriver64-260/64-bit_Driver/RPM
$ rpmextract.sh cndrvcups-capt-2.60-1.x86_64.rpm
$ cd ./usr/share/cups/model
$ cp ./CNCUPSLBP3100CAPTJ.ppd ~/

https://wiki.archlinux.org/index.php/Canon_CAPT

$ sudo pacman -S ghostscript gsfonts
$ sudo pacman -S system-config-printer
