1. Shrink windows partition

2. Create a new partition

3. Disable secure boot

4. Boot with USB

5. Connect to wireless network

$ wpa_supplicant -B -i wlo1 -c <(wpa_passphrase MYSSID passphrase)
$ dhcpcd wlo1

6. 

$ mkfs.ext4 /dev/mmcblk0p4
$ mount /dev/mmcblk0p4 /mnt
$ pacstrap /mnt base
$ genfstab -U /mnt >> /mnt/etc/fstab
$ arch-chroot /mnt

7. 

8.

$ pacman -S grub efibootmgr os-prober rsync wpa_supplicant arch-install-scripts
$ mkdir /efi
$ mount /dev/mmcblk0p1 /efi
$ grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=GRUB
$ os-prober
$ grub-mkconfig -o /boot/grub/grub.cfg

## SD card

$ mount /dev/sda2 /usr
$ mount /dev/sda3 /home
$ mount /dev/sda4 /var/work

## User
$ useradd user1
$ usermod -aG wheel user1

9. download econnman-1.1
$ pacman -S python-dbus connman
$ pip install python-efl

$ pacman -S xorg-xinput
$ xinput --list | grep Touch
$ xinput --list-props 12 | Tap
$ xinput --set-prop 12 286 1

$ pacman -S texlive-core texlive-bin texlive-fontsextra
$ pacman -S pandoc
$ pacman -S libreoffice-fresh
$ pacman -S noto-fonts-cjk

$ pacman -S fuse openntpd pacman-contrib deepin-screenshot code evince

## Notes

- Boot to firmware (EZ mode): Press F2 key and power on.

