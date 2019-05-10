---
layout: post
title: "Enable hibernation on Arch Linux"
---

How to enable hibernation on Arch Linux.

* Laptop: [ASUS X102BA](https://www.asus.com/Laptops/X102BA/)
* Dual boot: Arch Linux LTS and Windows 8

## Create a swap file

1. Check total memory size.

   ```
   $ free -h
                 total        used        free      shared  buff/cache   available
   Mem:          2.4Gi       619Mi       590Mi       2.0Mi       1.2Gi       1.6Gi
   Swap:            0B          0B          0B
   ```

2. Create a swap file.

   ```
   $ fallocate -l 2.4G /swapfile
   $ chmod 600 /swapfile
   $ mkswap /swapfile
   Setting up swapspace version 1, size = 2.4 GiB (2566909952 bytes)
   no label, UUID=78f84de2-2a78-4922-9ee7-5b0d7bedc590
   ```

3. Enable swap.

   ```  
   $ swapon /swapfile
   $ swapon -s
   Filename	Type	Size	Used	Priority
   /swapfile	file	2506748	0	-2
   $ free -b
                 total        used        free      shared  buff/cache   available
   Mem:          2.4Gi       622Mi       586Mi       2.0Mi       1.2Gi       1.6Gi
   Swap:         2.4Gi          0B       2.4Gi
   ```

4. Update `/etc/fstab`.

   ```
   /dev/sda5	/	ext4	rw,relatime,data=ordered	0 1
   /swapfile	none	swap	defaults			0 0
   ```

## Enable hibernation

1. Check the swap file offset.

   ```
   $ filefrag -v /swapfile
   Filesystem type is: ef53
   File size of /swapfile is 2566914048 (626688 blocks of 4096 bytes)
    ext:     logical_offset:        physical_offset: length:   expected: flags:
      0:        0..       0:   13469696..  13469696:      1:            
      1:        1..   14335:   13469697..  13484031:  14335:             unwritten
      2:    14336..   16383:   13486080..  13488127:   2048:   13484032: unwritten
   (more lines...)
   ```

2. Add kernel parameters to `/etc/default/grub` file.

   ```
   GRUB_CMDLINE_LINUX_DEFAULT="quiet resume=UUID=b196ea21-0496-4ff9-a7b2-97bee7bb1cd0 resume_offset=13469696"
   ```

3. Regenerate `/boot/grub/grub.cfg` file with above kernel parameters.

   ```
   $ os-prober
   /dev/sda1@/efi/Microsoft/Boot/bootmgfw.efi:Windows Boot Manager:Windows:efi
   $ grub-mkconfig -o /boot/grub/grub.cfg
   Generating grub configuration file ...
   Found linux image: /boot/vmlinuz-linux-lts
   Found initrd image: /boot/initramfs-linux-lts.img
   Found fallback initrd image(s) in /boot: initramfs-linux-lts-fallback.img
   Found linux image: /boot/vmlinuz-linux
   Found initrd image: /boot/initramfs-linux.img
   Found fallback initrd image(s) in /boot: initramfs-linux-fallback.img
   Found Windows Boot Manager on /dev/sda1@/efi/Microsoft/Boot/bootmgfw.efi
   done
   ```

4. Add "resume" after udev in `/etc/mkinitcpio.conf` file.
   
   ```
   HOOKS=(base udev resume autodetect modconf block filesystems keyboard fsck)
   ```
   
5. Regenerate the initramfs.

   ```
   $ mkinitcpio -p linux-lts
   ```

6. Test hibernation after reboot.

   ```
   $ systemctl hibernate
   ```

## Notes

* **systemd-swap** didn't work because hibernation needs a persistent fs blocks.
