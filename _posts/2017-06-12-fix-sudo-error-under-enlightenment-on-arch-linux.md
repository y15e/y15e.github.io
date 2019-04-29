---
layout: post
title: "Fix sudo error under Enlightenment on Arch Linux"
---

I got following error after update Arch Linux kernel to 4.11.2-1.

> sudo: effective uid is not 0, is /usr/bin/sudo on a file system with the 'nosuid' option set or an NFS file system without root privileges?

## How to fix this error:

1. Clone the linux kernel package.

   ```
   git clone https://git.archlinux.org/svntogit/packages.git --single-branch -b packages/linux kernel
   ```

2. Download the patch file and save to "kernel" directory.

   [linux-ptrace-fix.patch](https://bugs.archlinux.org/task/54170?getfile=15254)

3. The "kernel" directory looks like this.

   ```
   kernel/linux-ptrace-fix.patch
   kernel/trunk/90-linux.hook
   kernel/trunk/PKGBUILD
   kernel/trunk/config.i686
   kernel/trunk/config.x86_64
   kernel/trunk/linux.install
   kernel/trunk/linux.preset
   ```

4. Apply the patch.

   ```
   cd kernel
   patch -p1 -i linux-ptrace-fix.patch
   ```

5. Install xmlto package.

   ```
   sudo pacman -S xmlto
   ```

6. Import GPG keys of Linus Torvalds and Greg Kroah-Hartman.

   ```
   gpg2 --keyserver hkp://keys.gnupg.net --recv-keys 79BE3E4300411886
   gpg2 --keyserver hkp://keys.gnupg.net --recv-keys 38DBBDC86092693E
   ```

7. Build packages. (this will take long time.)

   ```
   cd trunk
   makepkg
   ```

8. Install the packages.

   ```
   sudo pacman -U linux-4.11.2-1-x86_64.pkg.tar.xz
   sudo pacman -U linux-headers-4.11.2-1-x86_64.pkg.tar.xz
   sudo pacman -U linux-docs-4.11.2-1-x86_64.pkg.tar.xz
   ```

9. Reboot the system.

## Notes:

* This sudo error was reported in below page.

  [Kernel 4.11.2 does not let user run su or sudo under Enlightenment](https://bugs.archlinux.org/task/54170)

* You will get following error if the GPG keys are not imported. (above step 6)

    ```
    ==> Verifying source file signatures with gpg...
        linux-4.11.tar ... FAILED (unknown public key 79BE3E4300411886)
        patch-4.11.2 ... FAILED (unknown public key 38DBBDC86092693E)
    ==> ERROR: One or more PGP signatures could not be verified!
    ```

* An alternative way to avoid the sudo error is using Linux LTS (Long Term Support) kernel.

  [Install the linux-lts package](https://wiki.archlinux.org/index.php/System_maintenance#Install_the_linux-lts_package)
