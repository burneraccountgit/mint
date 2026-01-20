# 1 
ZOEK VERSLEUTELDE PARTITIE
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
OPEN CONTAINER (DECRYPTIE)
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
- Kijk hoe de volumes heten onder de 'cryptdata' tak.
- Zoekt iets als: /dev/mapper/vgmint-root of /dev/mapper/mint--vg-root
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

# ERROR >> KERNEL PANIC! 
AGAIN
```
VFS: Unable to mount root fs on unknown-block(0,0)
```


---

Dit klinkt als een serieuze Kernel Panic, maar we weten precies wat de oorzaak is: de `initramfs` (het startbestand) mist of is corrupt, waardoor ik de versleutelde deur niet open krijg.

Omdat je workflow via GitHub en een Tablet loopt, heb ik de oplossing opgeknipt in **modulaire blokken**. Je kunt deze blokken één voor één kopiëren op je tablet, naar je repo sturen, en dan uitvoeren op je Live Mint omgeving.

Hier is je herstelplan in Obsidian MD formaat.

---

# Herstel Kernel Panic: Initramfs & GRUB Repair

> [!NOTE] Situatie
> **Fout:** `VFS: Unable to mount root fs on unknown-block(0,0)`
> 
> 
> **Oorzaak:** De kernel start, maar kan de versleutelde schijf niet openen omdat de `initramfs` ontbreekt.
> **Oplossing:** Via een `chroot` omgeving de `initramfs` opnieuw genereren.
> 
> 

---


## Module 0: Root Toegang 🛡️

```bash
# Word root (de prompt verandert van $ naar #)
sudo -i

# Controleer of je root bent (antwoord moet 'root' zijn)
whoami
```

### resultaat
```
mint@mint:~$ sudo -i
sudo: unable to allocate pty: No such device
mint@mint:~$ whoami
mint
mint@mint:~$ 
```

---

## Module 1: Schijven Koppelen 🔓

*Dit blok opent de versleuteling en koppelt de partities op de juiste plek.*

```bash
# 1. Open de versleutelde partitie
# Controleer of /dev/sda3 klopt via 'lsblk' of GParted.
sudo cryptsetup open /dev/sda3 cryptdata

# 2. Activeer LVM volumes
sudo vgchange -ay

# 3. Mount Root (systeem)
sudo mount /dev/mapper/vgmint-root /mnt

# 4. Mount Boot (kernel bestanden)
sudo mount /dev/sda2 /mnt/boot

# 5. Mount EFI (bootloader)
sudo mount /dev/sda1 /mnt/boot/efi

```

### resultaat
```
mint@mint:~$ # Bind mounts aanmaken voor systeemprocessen
for i in /dev /dev/pts /proc /sys /run; do sudo mount -B $i /mnt$i; done
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
mint@mint:~$ 
```

### resultaat
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


---

## Module 2: Voorbereiden Chroot 🛠️

*We koppelen de systeemmappen van de USB-stick aan je installatie, zodat updates denken dat ze op de echte PC draaien.*

```bash
# Bind mounts aanmaken voor systeemprocessen
for i in /dev /dev/pts /proc /sys /run; do sudo mount -B $i /mnt$i; done

```

### resultaat
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

### resultaat
```
mint@mint:~$ sudo mount --bind /dev /mnt/dev
sudo mount --bind /dev/pts /mnt/dev/pts
sudo mount --bind /proc /mnt/proc
sudo mount --bind /sys /mnt/sys
sudo mount --bind /run /mnt/run
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
mint@mint:~$ 
```

### resultaat
```
mint@mint:~$ # 1. Veiligheidshalve alles ontkoppelen (negeer fouten als het al los is)
sudo umount -R /mnt
sudo vgchange -an vgmint
sudo cryptsetup close cryptdata

# 2. Open Versleuteling
sudo cryptsetup open /dev/sda3 cryptdata
sudo vgchange -ay

# 3. Mount Systeempartities (Volgorde is cruciaal)
sudo mount /dev/mapper/vgmint-root /mnt
sudo mount /dev/sda2 /mnt/boot
sudo mount /dev/sda1 /mnt/boot/efi

# 4. Bind Systeemprocessen (Expliciet, geen loops)
sudo mount --bind /dev /mnt/dev
sudo mount --bind /dev/pts /mnt/dev/pts
sudo mount --bind /proc /mnt/proc
sudo mount --bind /sys /mnt/sys
sudo mount --bind /run /mnt/run

sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
mint@mint:~$ 
```


---

## Module 3: Chroot Binnengaan 💻

*Hiermee stappen we "in" je installatie op de harde schijf.*

```bash
# Wissel van USB-omgeving naar je harde schijf
sudo chroot /mnt

```

(Bron: )

> [!IMPORTANT]
> Na dit commando verandert je terminal prompt (bijv. naar `root@mint`). Vanaf nu voer je wijzigingen uit op je **echte systeem**.

---

## Module 4: De Reparatie (Initramfs & GRUB) 🩹

*Dit is de kern van de oplossing. We maken het ontbrekende bestand opnieuw aan.*

```bash
# 1. Genereer de initramfs opnieuw (Dit lost de 'unknown-block' error op)
update-initramfs -u -k all

# 2. Update GRUB voor de zekerheid
update-grub

```

(Bron: )

---

## Module 5: Afsluiten & Testen 🏁

*Alles netjes afsluiten om dataverlies te voorkomen.*

```bash
# 0. Kijk in de tabel die verschijnt naar de kolom Avail (of Beschikbaar). Hoeveel ruimte is daar nog vrij?
df -h /mnt/boot

# 1. Verlaat de chroot omgeving
exit

# 2. Ontkoppel alle partities
sudo umount -R /mnt

# 3. Sluit de LVM en encryptie
sudo vgchange -an vgmint
sudo cryptsetup close cryptdata

# 4. Herstarten
sudo reboot

```

(Bron: )

---

Zullen we, zodra je weer in je systeem kunt, kijken naar hoe we een backup van je `initramfs` kunnen maken voor de toekomst?

---

# ERROR >> KERNEL PANIC! 
AGAIN
```
VFS: Unable to mount root fs on unknown-block(0,0)
```

---

Het terugkeren van deze foutmelding bevestigt dat de vorige `initramfs` generatie is mislukt, waarschijnlijk door **ruimtegebrek op de boot-partitie** of een **corrupte kernel-installatie**. Als `/boot` vol zit (100%), wordt er een leeg bestand van 0 bytes geschreven, wat resulteert in `unknown-block(0,0)`.

We passen de strategie aan: we maken eerst ruimte, herstellen gebroken packages, en forceren dan een volledige herinstallatie van de kernel.

Hier zijn de modulaire blokken.

### Module 1: Systeem Koppelen & Binden

*Voer dit uit in de Live Mint omgeving om de schijf te openen.*

```bash
cryptsetup open /dev/sda3 cryptdata
vgchange -ay
mount /dev/mapper/vgmint-root /mnt
mount /dev/sda2 /mnt/boot
mount /dev/sda1 /mnt/boot/efi
for i in /dev /dev/pts /proc /sys /run; do mount -B $i /mnt$i; done

```

### Module 2: Chroot Starten

*Stap in de installatie.*

```bash
chroot /mnt

```

### Module 3: Diagnose & Ruimte Maken

*Controleer de ruimte en verwijder ongebruikte kernels om blokkades op te heffen.*

```bash
df -h /boot
apt-get clean
apt-get autoremove -y

```

### Module 4: Geforceerd Herstel Kernel

*In plaats van alleen updaten, installeren we de kernel opnieuw. Dit dwingt een correcte generatie van alle bestanden af.*

```bash
dpkg --configure -a
apt-get install --reinstall linux-image-generic linux-headers-generic
update-initramfs -u -k all
update-grub

```

### Module 5: Controle & Afsluiten

*Verifieer of het initrd bestand nu daadwerkelijk bestaat en groter is dan 0 bytes.*

```bash
ls -lh /boot/initrd.img*
exit
umount -R /mnt
vgchange -an vgmint
cryptsetup close cryptdata
reboot

```

### Vervolgstap

Controleer bij het uitvoeren van Module 3 de output van `df -h /boot`. Als het gebruikspercentage **100%** is en `autoremove` faalt, geef dit dan direct aan; dan moeten we handmatig oude kernels verwijderen met `rm`.
