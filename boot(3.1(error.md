```
mint@mint:~$ cryptsetup open /dev/sda3 cryptdata
vgchange -ay
mount /dev/mapper/vgmint-root /mnt
mount /dev/sda2 /mnt/boot
mount /dev/sda1 /mnt/boot/efi
for i in /dev /dev/pts /proc /sys /run; do mount -B $i /mnt$i; done
Device /dev/sda3 does not exist or access denied.
  WARNING: Running as a non-root user. Functionality may be unavailable.
  /run/lock/lvm/P_global:aux: open failed: Permission denied
mount: /mnt: must be superuser to use mount.
       dmesg(1) may have more information after failed mount system call.
mount: /mnt/boot: mount point does not exist.
       dmesg(1) may have more information after failed mount system call.
mount: /mnt/boot/efi: mount point does not exist.
       dmesg(1) may have more information after failed mount system call.
mount: /mnt/dev: mount point does not exist.
       dmesg(1) may have more information after failed mount system call.
mount: /mnt/dev/pts: mount point does not exist.
       dmesg(1) may have more information after failed mount system call.
mount: /mnt/proc: mount point does not exist.
       dmesg(1) may have more information after failed mount system call.
mount: /mnt/sys: mount point does not exist.
       dmesg(1) may have more information after failed mount system call.
mount: /mnt/run: mount point does not exist.
       dmesg(1) may have more information after failed mount system call.
mint@mint:~$ 
```
