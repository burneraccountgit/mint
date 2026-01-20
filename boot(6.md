Je logbestanden laten een kritiek probleem zien in je **Live Omgeving**: de foutmelding `sudo: unable to allocate pty` betekent dat je terminal-sessie corrupt is geraakt (waarschijnlijk door een verkeerde mount-actie in een eerdere poging).

Zolang deze fout er is, werkt **geen enkel** `sudo` commando en kun je niets herstellen.

### **Stap 0: Reset je Omgeving**

Voordat je onderstaande modules gebruikt:

1. **Sluit** je huidige terminalvenster.
2. **Open** een vers, nieuw terminalvenster.
3. Als de fout blijft terugkomen: **Herstart** de Live USB stick en begin vers.

Hier is het gecorrigeerde herstelplan. Ik heb een **"Module 0"** toegevoegd om direct root-rechten te krijgen. Dit voorkomt de `permission denied` fouten en elimineert de noodzaak om voor elk commando `sudo` te typen.

---

# Herstelplan: Kernel Panic & Full Boot Partition

> [!WARNING] Diagnose
> **Probleem:** De `initramfs` is corrupt (0 bytes) of ontbreekt.
> **Oorzaak:** Waarschijnlijk is je `/boot` partitie **100% vol**, waardoor het genereren van het startbestand halverwege afbreekt.
> **Doel:** Ruimte maken op `/boot` en de kernel geforceerd herinstalleren.

---

## Module 0: Root Toegang 🛡️

*We schakelen direct over naar de 'root' gebruiker. Dit voorkomt alle sudo-fouten.*

```bash
# Word root (de prompt verandert van $ naar #)
sudo -i

# Controleer of je root bent (antwoord moet 'root' zijn)
whoami

```

---

## Module 1: Schijven Koppelen 🔓

*Open de versleuteling en bereid de mounts voor.*

```bash
# 1. Open de versleutelde partitie
# (Vervang /dev/sda3 als je schijf anders heet, check met 'lsblk')
cryptsetup open /dev/sda3 cryptdata

# 2. Activeer de volumes
vgchange -ay

# 3. Mount de partities (Volgorde is belangrijk!)
mount /dev/mapper/vgmint-root /mnt
mount /dev/sda2 /mnt/boot
mount /dev/sda1 /mnt/boot/efi

# 4. Koppel systeemprocessen door (Bind mounts)
for i in /dev /dev/pts /proc /sys /run; do mount -B $i /mnt$i; done

```

---

## Module 2: Chroot Starten 💻

*Stap in je installatie op de harde schijf.*

```bash
# Wissel van USB-omgeving naar je systeem op schijf
chroot /mnt

```

> [!NOTE]
> Je terminal prompt verandert nu (bijv. naar `root@mint` of `root@...`). Je werkt nu op je harde schijf.

---

## Module 3: Ruimte Maken (Cruciaal) 🧹

*Hier lossen we de oorzaak op. We controleren de ruimte en verwijderen oude rommel.*

```bash
# 1. Controleer hoeveel ruimte er gebruikt wordt op /boot
# Als dit 100% is, is dit de gegarandeerde oorzaak van de crash.
df -h /boot

# 2. Probeer automatisch oude kernels en cache te verwijderen
apt-get clean
apt-get autoremove -y

```

> [!IMPORTANT]
> Als `apt-get autoremove` faalt met een foutmelding over "broken packages" of "no space left", stop dan hier en meld dit. We moeten dan handmatig één bestand verwijderen om de blokkade op te heffen.

---

## Module 4: Kernel Herstel 🩹

*Nu er ruimte is, dwingen we de computer om de kernel en initramfs vers en foutloos op te bouwen.*

```bash
# 1. Repareer eventuele half-geïnstalleerde pakketten
dpkg --configure -a

# 2. Herinstalleer de kernel (dit triggert het maken van initramfs)
apt-get install --reinstall linux-image-generic linux-headers-generic

# 3. Update initramfs voor de zekerheid (forceer overschrijven)
update-initramfs -u -k all

# 4. Update de bootloader
update-grub

```

---

## Module 5: Controle & Afsluiten 🏁

*Verifieer de reparatie en sluit netjes af.*

```bash
# 1. Check of het bestand nu wél bestaat (mag geen 0 bytes zijn!)
ls -lh /boot/initrd.img*

# 2. Verlaat de chroot
exit

# 3. Ontkoppel alles
umount -R /mnt
vgchange -an vgmint
cryptsetup close cryptdata

# 4. Herstarten (verwijder USB stick als daarom gevraagd wordt)
reboot

```
