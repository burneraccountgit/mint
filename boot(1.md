Om Boot Repair toegang te geven tot je versleutelde bestanden, moet je de container 'mappen' (openen) en de logische volumes activeren.

### PAYLOAD: UNLOCK & MOUNT LUKS

Voer deze regels regel voor regel uit in de terminal.

# 1. ZOEK JE VERSLEUTELDE PARTITIE
Zoek de grootste partitie, waarschijnlijk sda3 of nvme0n1p3.
```bash
lsblk
```

---

```bash
<pre>To run a command as administrator (user &quot;root&quot;), use &quot;sudo &lt;command&gt;&quot;.
See &quot;man sudo_root&quot; for details.

<font color="#8AE234"><b>mint@mint</b></font>:<font color="#729FCF"><b>~</b></font>$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
loop0    7:0    0   2.5G  1 loop /rofs
sda      8:0    0 978.1G  0 disk 
├─sda1   8:1    0   512M  0 part /mnt/boot-sav/sda1
├─sda2   8:2    0   1.7G  0 part /mnt/boot-sav/sda2
└─sda3   8:3    0 975.9G  0 part 
sdb      8:16   1   3.8G  0 disk 
└─sdb1   8:17   1   3.8G  0 part /cdrom
<font color="#8AE234"><b>mint@mint</b></font>:<font color="#729FCF"><b>~</b></font>$ 
</pre>
```

---
**Next Step:**
Als `lsblk` na stap 2 of 3 geen logische volumes (zoals `root`) laat zien, plak dan hier de output van `lsblk`, dan is de structuur anders (geen LVM).

---

# 1. Maak de 'boot-sav' mounts los (om conflicten te voorkomen)
```bash
sudo umount /mnt/boot-sav/sda1
sudo umount /mnt/boot-sav/sda2
```

# 1. MOUNT DE ROOT (Het versleutelde systeem)
```bash
sudo mount /dev/mapper/vgmint-root /mnt
```




---

# 2. OPEN DE CONTAINER (DECRYPTIE)
Vervang /dev/sdXY door jouw encrypted partitie (bv. /dev/sda3)
'cryptdata' is de naam die we het tijdelijk geven.
```bash
sudo cryptsetup open /dev/sdXY cryptdata
```
## (Voer je wachtwoord in als erom gevraagd wordt)

# 2. Open de versleutelde container (sda3)
```bash
sudo cryptsetup open /dev/sda3 cryptdata
```
(Typ je wachtwoord blind in en druk op Enter)


# 2. MOUNT DE BOOT PARTITIE (sda2 - 1.7G)
Deze bevat je kernels en initramfs images
```bash
sudo mount /dev/sda2 /mnt/boot
```







---

# 3. ACTIVEER LVM (CRUCIAAL BIJ MINT)
Mint gebruikt standaard LVM binnenin de encryptie.
Dit commando scant en activeert de volumes (zoals 'root' en 'swap').
```bash
sudo vgchange -ay
```

# 3. Activeer de interne LVM volumes
```bash
sudo vgchange -ay
```

# 3. MOUNT DE EFI PARTITIE (sda1 - 512M)
Deze bevat de bootloader (GRUB/Shim) voor UEFI
```bash
sudo mount /dev/sda1 /mnt/boot/efi
```








---

# 4. CONTROLEER DE MAPPER PADEN
Kijk nu hoe de volumes heten onder de 'cryptdata' tak.
```bash
lsblk
```
Je zoekt iets als: /dev/mapper/vgmint-root of /dev/mapper/mint--vg-root

# 4. Toon de nieuwe situatie
```bash
lsblk
```


```bash
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

mint@mint:~$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
loop0    7:0    0   2.5G  1 loop /rofs
sda      8:0    0 978.1G  0 disk 
├─sda1   8:1    0   512M  0 part /mnt/boot-sav/sda1
├─sda2   8:2    0   1.7G  0 part /mnt/boot-sav/sda2
└─sda3   8:3    0 975.9G  0 part 
sdb      8:16   1   3.8G  0 disk 
└─sdb1   8:17   1   3.8G  0 part /cdrom
mint@mint:~$ sudo umount /mnt/boot-sav/sda1
mint@mint:~$ sudo umount /mnt/boot-sav/sda2
mint@mint:~$ sudo cryptsetup open /dev/sda3 cryptdata
Enter passphrase for /dev/sda3: 
mint@mint:~$ sudo vgchange -ay
  2 logical volume(s) in volume group "vgmint" now active
mint@mint:~$ sudo vgchange -ay
  2 logical volume(s) in volume group "vgmint" now active
mint@mint:~$ lsblk
NAME                MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINTS
loop0                 7:0    0   2.5G  1 loop  /rofs
sda                   8:0    0 978.1G  0 disk  
├─sda1                8:1    0   512M  0 part  
├─sda2                8:2    0   1.7G  0 part  
└─sda3                8:3    0 975.9G  0 part  
  └─cryptdata       252:0    0 975.9G  0 crypt 
    ├─vgmint-root   252:1    0 929.4G  0 lvm   
    └─vgmint-swap_1 252:2    0   1.9G  0 lvm   
sdb                   8:16   1   3.8G  0 disk  
└─sdb1                8:17   1   3.8G  0 part  /cdrom
mint@mint:~$ 
```

```bash

<pre><font color="#8AE234"><b>mint@mint</b></font>:<font color="#729FCF"><b>~</b></font>$ sudo mount /dev/mapper/vgmint-root /mnt
<font color="#8AE234"><b>mint@mint</b></font>:<font color="#729FCF"><b>~</b></font>$ sudo mount /dev/sda2 /mnt/boot
<font color="#8AE234"><b>mint@mint</b></font>:<font color="#729FCF"><b>~</b></font>$ sudo mount /dev/sda1 /mnt/boot/efi
<font color="#8AE234"><b>mint@mint</b></font>:<font color="#729FCF"><b>~</b></font>$ 

</pre>
```


# boot repair
```
Boot successfully repaired.

A new file (/var/log/boot-repair/20260120_082535/Boot-Info_20260120_0825.txt) will open in your text viewer.


In case you still experience boot problem, indicate its content to:
boot.repair@gmail.com or to your favorite support forum.

You can now reboot your computer.
```




# 4. START BOOT REPAIR
Nu alles gemount is op /mnt, kan de tool (of terminal) erbij.
```bash
boot-repair
```




---

# 5. MOUNT DE ROOT PARTITIE
Vervang het pad hieronder met wat je bij stap 4 vond.
```bash
sudo mount /dev/mapper/vgmint-root /mnt
```


---

# 6. MOUNT DE BOOT PARTITIE (Indien apart)
Boot Repair heeft vaak ook de /boot partitie nodig.
Dit is vaak de partitie direct boven je encrypted partitie (bv sda2).
```bash
sudo mount /dev/sdXZ /mnt/boot
```

---

# NU KAN JE BOOT REPAIR STARTEN

```


