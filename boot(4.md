*To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.*
---



# 1 
ZOEK JE VERSLEUTELDE PARTITIE
```
mint@mint:~$ lsblk
<pre><font color="#8AE234"><b>mint@mint</b></font>:<font color="#729FCF"><b>~</b></font>$ lsblk
NAME                MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINTS
loop0                 7:0    0   2.5G  1 loop  /rofs
sda                   8:0    0 978.1G  0 disk  
├─sda1                8:1    0   512M  0 part  /mnt/boot/efi
├─sda2                8:2    0   1.7G  0 part  /mnt/boot
└─sda3                8:3    0 975.9G  0 part  
  └─cryptdata       252:0    0 975.9G  0 crypt 
    ├─vgmint-root   252:1    0 929.4G  0 lvm   /mnt
    └─vgmint-swap_1 252:2    0   1.9G  0 lvm   
sdb                   8:16   1   3.8G  0 disk  
└─sdb1                8:17   1   3.8G  0 part  /cdrom
<font color="#8AE234"><b>mint@mint</b></font>:<font color="#729FCF"><b>~</b></font>$ 
</pre>
mint@mint:~$
```



# 2
OPEN DE CONTAINER (DECRYPTIE)
```
sudo cryptsetup open /dev/sda3 cryptdata
```



# 3
ACTIVEER LVM (CRUCIAAL BIJ MINT)
- Mint gebruikt standaard LVM binnenin de encryptie.
- Dit commando scant en activeert de volumes (zoals 'root' en 'swap').
```
sudo vgchange -ay
```



# 4
CONTROLEER DE MAPPER PADEN
- Kijk nu hoe de volumes heten onder de 'cryptdata' tak.
- Je zoekt iets als: /dev/mapper/vgmint-root of /dev/mapper/mint--vg-root
```
mint@mint:~$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
loop0    7:0    0   2.5G  1 loop /rofs
sda      8:0    0 978.1G  0 disk 
├─sda1   8:1    0   512M  0 part /mnt/boot-sav/sda1
├─sda2   8:2    0   1.7G  0 part /mnt/boot-sav/sda2
└─sda3   8:3    0 975.9G  0 part 
sdb      8:16   1   3.8G  0 disk 
└─sdb1   8:17   1   3.8G  0 part /cdrom
```



# 5
