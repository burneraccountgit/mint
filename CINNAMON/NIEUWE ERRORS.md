# FIRST OF ALL IK DACHT TOCH ECHT MINT 22.3 TE HEBBEN INSTALLED..DUS WAAROM GEEFT DE DPKG 6.14 AAN GODVERDOMME!!!

```
ys@msi:~$ sudo -i
[sudo] password for ys:       
root@msi:~# df -h /boot
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2       1.7G  1.6G     0 100% /boot
root@msi:~# sudo apt-get autoremove --purge
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
1 not fully installed or removed.
After this operation, 0 B of additional disk space will be used.
Setting up initramfs-tools (0.142ubuntu25.5) ...
update-initramfs: deferring update (trigger activated)
Processing triggers for initramfs-tools (0.142ubuntu25.5) ...
update-initramfs: Generating /boot/initrd.img-6.14.0-37-generic
I: The initramfs will attempt to resume from /dev/dm-2
I: (/dev/mapper/vgmint-swap_1)
I: Set the RESUME variable to override this.
cat: write error: No space left on device
update-initramfs: failed for /boot/initrd.img-6.14.0-37-generic with 1.
dpkg: error processing package initramfs-tools (--configure):
 installed initramfs-tools package post-installation script subprocess returned error exit status 1
Errors were encountered while processing:
 initramfs-tools
E: Sub-process /usr/bin/dpkg returned an error code (1)
root@msi:~# df -h /boot
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2       1.7G  1.6G     0 100% /boot
root@msi:~# df -h /boot
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2       1.7G  1.6G     0 100% /boot
root@msi:~# sudo apt-get autoremove --purge
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
1 not fully installed or removed.
After this operation, 0 B of additional disk space will be used.
Setting up initramfs-tools (0.142ubuntu25.5) ...
update-initramfs: deferring update (trigger activated)
Processing triggers for initramfs-tools (0.142ubuntu25.5) ...
update-initramfs: Generating /boot/initrd.img-6.14.0-37-generic
I: The initramfs will attempt to resume from /dev/dm-2
I: (/dev/mapper/vgmint-swap_1)
I: Set the RESUME variable to override this.
cat: write error: No space left on device
update-initramfs: failed for /boot/initrd.img-6.14.0-37-generic with 1.
dpkg: error processing package initramfs-tools (--configure):
 installed initramfs-tools package post-installation script subprocess returned error exit status 1
Errors were encountered while processing:
 initramfs-tools
E: Sub-process /usr/bin/dpkg returned an error code (1)
root@msi:~# dpkg --list | grep linux-image
ii  linux-image-6.14.0-37-generic              6.14.0-37.37~24.04.1                       amd64        Signed kernel image generic
ii  linux-image-generic-hwe-24.04              6.14.0-37.37~24.04.1                       amd64        Generic Linux kernel image
root@msi:~# 

```

