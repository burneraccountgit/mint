# MODULE 1
```
mint@mint:~$ # 1. Open de versleutelde partitie met root-rechten
sudo cryptsetup open /dev/sda3 cryptdata

# 2. Activeer LVM volumes
sudo vgchange -ay

# 3. Mount Root (systeem)
sudo mount /dev/mapper/vgmint-root /mnt

# 4. Mount Boot en EFI
sudo mount /dev/sda2 /mnt/boot
sudo mount /dev/sda1 /mnt/boot/efi

# 5. Bind systeem mappen (nodig voor chroot)
for i in /dev /dev/pts /proc /sys /run; do sudo mount -B $i /mnt$i; done
Enter passphrase for /dev/sda3: 
  2 logical volume(s) in volume group "vgmint" now active
```



# MODULE 2
```
mint@mint:~$ # Bind mounts aanmaken voor systeemprocessen
for i in /dev /dev/pts /proc /sys /run; do sudo mount -B $i /mnt$i; done
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
mint@mint:~$ 
```
