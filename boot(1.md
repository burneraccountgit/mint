Om Boot Repair toegang te geven tot je versleutelde bestanden, moet je de container 'mappen' (openen) en de logische volumes activeren.

### PAYLOAD: UNLOCK & MOUNT LUKS

Voer deze regels regel voor regel uit in de terminal.

```bash
# 1. ZOEK JE VERSLEUTELDE PARTITIE
# Zoek de grootste partitie, waarschijnlijk sda3 of nvme0n1p3.
lsblk

---

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

---
**Next Step:**
Als `lsblk` na stap 2 of 3 geen logische volumes (zoals `root`) laat zien, plak dan hier de output van `lsblk`, dan is de structuur anders (geen LVM).

---

# Maak de 'boot-sav' mounts los (om conflicten te voorkomen)
sudo umount /mnt/boot-sav/sda1
sudo umount /mnt/boot-sav/sda2


---

# 2. OPEN DE CONTAINER (DECRYPTIE)
# Vervang /dev/sdXY door jouw encrypted partitie (bv. /dev/sda3)
# 'cryptdata' is de naam die we het tijdelijk geven.
sudo cryptsetup open /dev/sdXY cryptdata
# (Voer je wachtwoord in als erom gevraagd wordt)


---

# 3. ACTIVEER LVM (CRUCIAAL BIJ MINT)
# Mint gebruikt standaard LVM binnenin de encryptie.
# Dit commando scant en activeert de volumes (zoals 'root' en 'swap').
sudo vgchange -ay

---

# 4. CONTROLEER DE MAPPER PADEN
# Kijk nu hoe de volumes heten onder de 'cryptdata' tak.
lsblk
# Je zoekt iets als: /dev/mapper/vgmint-root of /dev/mapper/mint--vg-root

---

# 5. MOUNT DE ROOT PARTITIE
# Vervang het pad hieronder met wat je bij stap 4 vond.
sudo mount /dev/mapper/vgmint-root /mnt

---

# 6. MOUNT DE BOOT PARTITIE (Indien apart)
# Boot Repair heeft vaak ook de /boot partitie nodig.
# Dit is vaak de partitie direct boven je encrypted partitie (bv sda2).
sudo mount /dev/sdXZ /mnt/boot


---

# NU KAN JE BOOT REPAIR STARTEN

```


