De foutmeldingen "Permission denied" en "must be superuser" geven aan dat de commando's **beheerdersrechten** (root) missen. In een Live omgeving moet je overal `sudo` voor zetten.

Doordat de eerste commando's faalden, werd de hoofdschijf niet gekoppeld op `/mnt`, waardoor de mappen `/mnt/boot` en `/mnt/dev` nog niet bestaan. Dat veroorzaakte de waterval aan foutmeldingen daarna.

Hier is **Module 1** gecorrigeerd met `sudo` voor elk commando.

### Module 1: Systeem Koppelen (Gecorrigeerd) 🔓

*Voer dit blok uit om de toegang te forceren. Als `/dev/sda3` niet gevonden wordt, kan het zijn dat je schijf een andere naam heeft (bijv. `nvme0n1p3`), maar meestal is het een kwestie van rechten.*

```bash
# 1. Open de versleutelde partitie met root-rechten
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

```

Zodra dit zonder foutmeldingen is uitgevoerd, kun je direct door naar **Module 2** (Chroot Starten) uit het vorige bericht.

Wil je dat ik Module 2 en verder ook even opnieuw uitschrijf met `sudo` voor de zekerheid, of heb je die nog bij de hand?
