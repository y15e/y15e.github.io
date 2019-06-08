1. Shrink windows partition

2. Create a new partition

3. Disable secure boot

4. Boot with USB

5. Connect to wireless network

$ wpa_supplicant -B -i wlo1 -c <(wpa_passphrase MYSSID passphrase)
$ dhcpcd wlo1

6. 

$ mkfs.ext4 /dev/mm~

7. 

$ pacstrap

8.
$ mkdir /efi
$ mount /dev/mmcblk0p1 /efi
$ grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=GRUB
$ os-prober
$ grub-mkconfig -o /boot/grub/grub.cfg

9. pip install python-efl
10. download econnman-1.1

$ pacman -S xorg-xinput
$ xinput --list
$ xinput --list-props 12
$ xinput --set-prop 12 286 1
