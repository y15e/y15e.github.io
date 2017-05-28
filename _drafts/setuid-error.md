---
layout: post
title: ""
---


```
sudo: effective uid is not 0, is /usr/bin/sudo on a file system with the 'nosuid' option set or an NFS file system without root privileges?
```

https://bugs.archlinux.org/task/54170

patch file
https://bugs.archlinux.org/task/54170?getfile=15254

how to apply patch
https://wiki.archlinux.org/index.php/Patching_in_ABS#Applying_patches

```
==> Verifying source file signatures with gpg...
    linux-4.11.tar ... FAILED (unknown public key 79BE3E4300411886)
    patch-4.11.2 ... FAILED (unknown public key 38DBBDC86092693E)
==> ERROR: One or more PGP signatures could not be verified!
```

in PKGBUILD file
```
validpgpkeys=(
              'ABAF11C65A2970B130ABE3C479BE3E4300411886' # Linus Torvalds
              '647F28654894E3BD457199BE38DBBDC86092693E' # Greg Kroah-Hartman
             )
```

https://www.kernel.org/signature.html

gpg2 --keyserver hkp://keys.gnupg.net --recv-keys 79BE3E4300411886
gpg2 --keyserver hkp://keys.gnupg.net --recv-keys 38DBBDC86092693E

```
  # add upstream patch
  patch -p1 -i "${srcdir}/patch-${pkgver}"
  patch -p1 -i "${srcdir}/linux-ptrace-fix.patch"
```

work/linux/linux-ptrace-fix.patch
work/linux/trunk/PKGBUILD
work/linux/trunk/90-linux.hook
work/linux/trunk/config.i686
work/linux/trunk/config.x86_64
work/linux/trunk/linux.install
work/linux/trunk/linux.preset

```
patch -p1 -i linux-ptrace-fix.patch
```

sudo pacman -U 