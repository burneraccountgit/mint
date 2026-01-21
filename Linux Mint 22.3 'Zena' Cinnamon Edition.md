Linux Mint 22.3 'Zena' Cinnamon Edition.md
IK VERTROUW MIJN SYSTEEM MOMENTEEL NIET
IK WIL KERNEL PANIC OP ONORTHODOXE WIJZE FIXEN
IK ZIT NU IN LIVE BOOT ONLINE
IK WIL DE GENOEMDE 22.3 VERSIE ALS KERNEL INSTALLEREN 
IK WIL MIJN BESTANDEN EN PROGRAMMAS EN INSTELLINGEN HOUDEN EN BEHOUDEN
IK HEB MOMENTEEL UBUNTU'S INSTALLED ALSOOK MINT VERSIES 6.8 EN 6.14
IK WIL DIE UBUNTU INSTALLS VERWIJDEREN NET ALS DE MINT VERSIES 6.8 EN 6.14
MAAR NIET DAN NADAT IK EERST VIA LIVE BOOT DE 22.3 VERSIE VAN MINT INSTALLED HEB

EN IK WIL NIET DOMWEG COMMANDOS UITVOEREN EN MILJARD KEER REBOOTEN BIJ ELKE NIEUWE ERROR WAAR JIJ GEEN REKENING MEE HOUDT EN VERVOLGENS MIJ DE SCHULD VAN GEEFT DAT IK "IETS" VERGETEN ZOU ZIJN. 

KAN JE DAT JA OF NEE? IK WIL MODULAR WERKEN DUS IK WIL NIET DAT JE BEGINT MET 10000000 MODULES WANT IK LOOP TOCH BIJ DE EERSTE MODULE _ZOALS ALTIJD_ VAST MET ERRORS. 

ALSO IK WIL EERST VOLLEDIGE VERZAMELING VAN GEGEVENS ZODAT JE GEEN STUPIDE AANNAMES GAAT DOEN OVER WAARSCHIJNLIJKHEDEN DIE ALTIJD ANDERS BLEKEN DAN DAT JIJ AANNAM. 

FURTHERMORE WIL IK EERST BACKUP MAKEN VAN AL MIJN BESTANDEN PROGRAMMA'S EN INSTELLINGEN OP MIJN SSD

DAN WIL IK HELE SCHIJF VAN PC WISSEN

DAN WIL IK EENVOUDIG SSD TERUGZETTEN EN AL MIJN BESTANDEN, AL MIJN PROGRAMMA'S ZOALS IK ZE HAD INGESTELD, ALSOOK AL MIJN WIDGETS EN DERGELIJKE ALLEMAAL TERUG HEBBEN, ÁLLES!!! 

IMMERS ALS WE SLECHTS DE KERNEL UPGRADEN EN UPDATEN DAN MOET ER BOVEN DE MOTORKAP ALLES HETZELFDE KUNNEN BLIJVEN LIJKT MIJ



---

```bash

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

mint@mint:~$ lsblk -f
NAME   FSTYPE      FSVER LABEL      UUID                                 FSAVAIL FSUSE% MOUNTPOINTS
loop0  squashfs    4.0                                                         0   100% /rofs
sda                                                                                     
├─sda1 vfat        FAT32            C535-0B9E                                           
├─sda2 ext4        1.0              4588079c-fc78-42a7-bf9a-86c700b12ca5                
└─sda3 crypto_LUKS 2                279a2ae4-af1e-4985-8976-f2535b89b7e9                
sdb                                                                                     
└─sdb1 vfat        FAT32 LINUX MINT 8C3F-9CA2                             974.3M    75% /cdrom
mint@mint:~$ sudo fdisk -l
Disk /dev/loop0: 2.45 GiB, 2633056256 bytes, 5142688 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/sda: 978.09 GiB, 1050214588416 bytes, 2051200368 sectors
Disk model: Crucial_CT1050MX
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 899E027A-3F7B-45E7-A0AB-5B8A501BB414

Device       Start        End    Sectors   Size Type
/dev/sda1     2048    1050623    1048576   512M EFI System
/dev/sda2  1050624    4550655    3500032   1.7G Linux filesystem
/dev/sda3  4550656 2051198975 2046648320 975.9G Linux filesystem


Disk /dev/sdb: 3.84 GiB, 4126146560 bytes, 8058880 sectors
Disk model: TransMemory     
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x14116ac5

Device     Boot Start     End Sectors  Size Id Type
/dev/sdb1  *     2048 8058863 8056816  3.8G  c W95 FAT32 (LBA)
mint@mint:~$ 

```

Dit is een complexe operatie omdat je een "Clean Wipe" wilt combineren met het behoud van een bestaande configuratie (bestanden, programma's en tweaks). In Linux zijn programma's en instellingen echter diep verweven met de systeembestanden en pakketbronnen.

Om te voorkomen dat we halverwege vastlopen op aannames, gaan we dit in fasen doen. Ik begin niet met commando's. We beginnen met de **Inventarisatie**.

### Fase 1: Systeem Inventarisatie (De Nulmeting)

Voordat we iets back-uppen of wissen, moet ik exact weten hoe de data verdeeld is. Draai de volgende commando's in de terminal van je **Live Boot** en kopieer de output hierheen.

```bash
lsblk -o NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL

```

*Doel: Identificeren welke partitie je huidige Mint-installatie is en waar je SSD (voor backup) zich bevindt.*

```bash
sudo parted -l

```

*Doel: Vaststellen of we met GPT/EFI of MBR/Legacy te maken hebben. Dit is cruciaal voor het herstellen van de bootloader later.*

```bash
ls /mnt/etc/apt/sources.list.d/

```

*(Eerst de juiste partitie mounten naar /mnt). Doel: Zien welke PPA's en externe repo's je gebruikt, zodat je programma's later ook echt terugkomen.*

---

### Het Plan van Aanpak (Strategie)

Om te bereiken wat jij wilt zonder "miljard reboots", is de meest stabiele methode:

1. **De 'State' isoleren:** We trekken een lijst van alle geïnstalleerde pakketten (`dpkg --get-selections`) en we maken een rsync-kopie van je `/home` folder (instellingen + bestanden) naar de SSD.
2. **Configuratie veiligstellen:** We kopiëren `/etc/` handmatig naar de SSD. Hierin staan je systeeminstellingen, wifi-wachtwoorden en fstab.
3. **De Harde Reset:** We wissen de hele schijf en installeren Mint 22.3 'Zena' vers van de Live USB.
4. **De Injectie:** We injecteren je pakketlijst en je `/home` folder terug in de nieuwe installatie. Omdat de kernel (onder de motorkap) losstaat van je home-configuratie (boven de motorkap), blijven je widgets en instellingen behouden op de nieuwe basis.

### Waarschuwing over "Programma's"

Bestanden en instellingen (widgets, wallpaper, browser-data) zijn makkelijk. **Programma's** zelf kunnen niet simpelweg "teruggezet" worden door een map te kopiëren; ze moeten via de package manager van 22.3 opnieuw worden geïnstalleerd op basis van je lijst om compatibiliteit met de nieuwe bibliotheken te garanderen.

**Stap 1 voor jou:**
Geef me de output van de bovenstaande `lsblk` en `parted -l` commando's. Zodra ik die heb, bepaal ik de exacte mount-commando's voor je backup.

Wil je dat ik eerst een script voor je maak dat de inventarisatie van je geïnstalleerde programma's automatiseert naar een tekstbestand op je SSD?

---

```
mint@mint:~$ lsblk -o NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL
NAME   FSTYPE        SIZE MOUNTPOINT              LABEL
loop0  squashfs      2.5G /rofs                   
sda                978.1G                         
├─sda1 vfat          512M                         
├─sda2 ext4          1.7G                         
└─sda3 crypto_LUKS 975.9G                         
sdb                  3.8G                         
└─sdb1 vfat          3.8G /cdrom                  LINUX MINT
sdc                931.5G                         
└─sdc1 exfat       931.5G /media/mint/USB-STAAFJE USB-STAAFJE
mint@mint:~$ sudo parted -l
Model: ATA Crucial_CT1050MX (scsi)
Disk /dev/sda: 1050GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags: 

Number  Start   End     Size    File system  Name                  Flags
 1      1049kB  538MB   537MB   fat32        EFI System Partition  boot, esp
 2      538MB   2330MB  1792MB  ext4
 3      2330MB  1050GB  1048GB


Model: TOSHIBA TransMemory (scsi)
Disk /dev/sdb: 4126MB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags: 

Number  Start   End     Size    Type     File system  Flags
 1      1049kB  4126MB  4125MB  primary  fat32        boot, lba


Model: Samsung Portable SSD T5 (scsi)
Disk /dev/sdc: 1000GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags: 

Number  Start   End     Size    Type     File system  Flags
 1      1000kB  1000GB  1000GB  primary


mint@mint:~$ ls /mnt/etc/apt/sources.list.d/
ls: cannot access '/mnt/etc/apt/sources.list.d/': No such file or directory
mint@mint:~$ 
```

---

Helder. De data is binnen. We hebben een kritiek punt gevonden: **`/dev/sda3` is versleuteld (LUKS).** Dit is de reden waarom `/mnt` leeg was; we moeten de "kluis" eerst openen voordat we bij je bestanden en instellingen kunnen voor de backup.

Ik ga nu niet 100 commando's geven. We doen alleen de **Ontsluiting** en de **Data-Check**.

### Stap 1: De versleutelde schijf openen

Omdat je in een Live Boot zit, is de schijf nog vergrendeld. Voer dit uit om toegang te krijgen tot je eigenlijke systeem:

```bash
sudo cryptsetup luksOpen /dev/sda3 mijn_systeem

```

*(Er wordt nu om je wachtwoord gevraagd van je schijfversleuteling).*

### Stap 2: Mounten en Locatie bepalen

Nu de schijf open is, moeten we de partitie koppelen om te zien waar je `/home` en `/etc` staan.

```bash
sudo mount /dev/mapper/mijn_systeem /mnt

```

### Stap 3: De bronnenlijst checken (Opnieuw)

Nu de schijf gemount is, kunnen we wel in de mappen kijken. Voer deze uit:

```bash
ls /mnt/etc/apt/sources.list.d/

```

### Waarom dit de enige manier is

Omdat je de hele schijf wilt wissen en Mint 22.3 wilt installeren, maar je instellingen wilt behouden, moeten we nu we toegang hebben drie dingen veiligstellen op je **Samsung SSD (sdc1)**:

1. De lijst met programma's die je nu hebt.
2. De map `/mnt/home/[jouw-gebruikersnaam]` (hierin zitten je widgets, bureaublad, browserprofielen).
3. De map `/mnt/etc/` (voor systeem-brede configuraties).

---

**De status op dit moment:**

* Je hebt een GPT/EFI systeem (moderne standaard).
* Je backup-schijf (`sdc1`) is `exfat`. Dit is prima voor bestanden, maar **slecht** voor Linux-rechten. We gaan de backup daarom in een `.tar` archief zetten zodat je instellingen (rechten) niet kapot gaan op die Samsung schijf.

**Zodra je de output van de `ls /mnt/etc/apt/sources.list.d/` geeft, weet ik of je speciale software-bronnen hebt waar we rekening mee moeten houden. Lukt het openen van de schijf met het eerste commando?**

---

```
mint@mint:~$ sudo cryptsetup luksOpen /dev/sda3 mijn_systeem
Enter passphrase for /dev/sda3: 
mint@mint:~$ sudo mount /dev/mapper/mijn_systeem /mnt
mount: /mnt: unknown filesystem type 'LVM2_member'.
       dmesg(1) may have more information after failed mount system call.
mint@mint:~$ ls /mnt/etc/apt/sources.list.d/
ls: cannot access '/mnt/etc/apt/sources.list.d/': No such file or directory
mint@mint:~$ 
```

---

Je systeem gebruikt **LVM (Logical Volume Management)** bovenop de versleuteling. Dat is de standaard "Advanced Installation" van Mint/Ubuntu. De foutmelding `unknown filesystem type 'LVM2_member'` betekent dat we de logische volumes binnen de versleutelde container moeten activeren voordat we ze kunnen mounten.

We gaan dit nu direct oplossen zodat we bij je bestanden kunnen.

### Stap 1: Activeer de LVM Volumes

Voer dit commando uit om de volumes zichtbaar te maken voor het systeem:

```bash
sudo vgscan && sudo vgchange -ay

```

### Stap 2: Identificeer het Root Volume

Nu moeten we kijken hoe de volumes heten. Meestal is het iets als `vgmint-root`.

```bash
ls /dev/mapper/

```

### Stap 3: De juiste mount poging

Kijk in de output van het vorige commando naar iets dat eindigt op `-root`. Gebruik die naam in het volgende commando (vervang `NAAM_VAN_ROOT` door wat je ziet, bijvoorbeeld `vgmint-root`):

```bash
sudo mount /dev/mapper/NAAM_VAN_ROOT /mnt

```

---

### Controleer daarna direct de bronnenlijst:

Als de mount is gelukt, voer je deze weer uit:

```bash
ls /mnt/etc/apt/sources.list.d/

```

**Waarom dit essentieel is voor je plan:**
Omdat je een "Clean Wipe" wilt doen en daarna alles terug wilt zetten, moeten we exact weten welke LVM-structuur je nu hebt. Als we straks Mint 22.3 installeren, moet ik weten of je weer LVM+LUKS wilt, of dat we overstappen naar een simpelere indeling.

**Geef me de output van `ls /dev/mapper/` en laat weten of de mount is gelukt.**

---

```
mint@mint:~$ sudo vgscan && sudo vgchange -ay
  Found volume group "vgmint" using metadata type lvm2
  2 logical volume(s) in volume group "vgmint" now active
mint@mint:~$ ls /dev/mapper/
control  mijn_systeem  vgmint-root  vgmint-swap_1
mint@mint:~$ sudo mount /dev/mapper/vgmint-root /mnt
mint@mint:~$ ls /mnt/etc/apt/sources.list.d/
google-chrome.list  official-package-repositories.list  sunderme-texstudio-noble.list
mint@mint:~$ 
```

---

De kluis is open en we hebben toegang tot de data. We zien nu dat je Google Chrome en TeXstudio (Noble/Ubuntu 24.04 basis) als extra bronnen hebt.

Omdat je een **volledige schijfwipe** wilt en daarna **álle** instellingen en programma's terug wilt zonder compatibiliteitsproblemen, gaan we nu de backup-fase in. We gebruiken je Samsung SSD (`/media/mint/USB-STAAFJE`) als kluis voor je huidige systeem.

Voer de volgende module uit om alle noodzakelijke gegevens en bestanden te verzamelen.

### Module: Full State Export

Dit script doet drie dingen: het maakt een lijst van je programma's, back-upt je systeemconfiguratie (`/etc`) en verpakt je volledige gebruikersomgeving inclusief widgets en verborgen instellingen in één groot archief op je SSD.

```bash
# 1. Maak een backup-map aan op de Samsung SSD
mkdir -p /media/mint/USB-STAAFJE/MINT_BACKUP

# 2. Exporteer de lijst met geïnstalleerde programma's
chroot /mnt dpkg --get-selections > /media/mint/USB-STAAFJE/MINT_BACKUP/pakketlijst.txt

# 3. Backup de systeemconfiguratie (APT bronnen, fstab, etc.)
sudo tar -cvpzf /media/mint/USB-STAAFJE/MINT_BACKUP/system_config.tar.gz /mnt/etc

# 4. Backup je volledige Home-folder (Bestanden + Instellingen + Widgets)
# LET OP: Dit kan even duren afhankelijk van de hoeveelheid data.
sudo tar -cvpzf /media/mint/USB-STAAFJE/MINT_BACKUP/user_home_backup.tar.gz -C /mnt/home .

```

### Waarom we dit zo doen:

* **`.tar.gz`:** Je Samsung SSD is `exfat`. Als we bestanden los zouden kopiëren, verlies je alle Linux-permissies (wie mag welk bestand lezen). In een tar-archief blijven deze permissies **binnen** het pakketje bewaard. Dit is de enige manier om je widgets en instellingen werkend terug te krijgen.
* **`dpkg --get-selections`:** Dit is je boodschappenlijstje. Straks vertellen we Mint 22.3: "Installeer alles wat op deze lijst staat".

**Actie:** Voer deze blokken uit. Laat me weten als de terminal weer beschikbaar is (als de `tar` commando's klaar zijn).

**Vraag ter controle voordat we de schijf wissen in de volgende stap:**
Staan er op `/dev/sda2` (je huidige `/boot` partitie) nog specifieke bestanden die je handmatig hebt aangepast, of mag die ook integraal gewist worden bij de herinstallatie?

---

# ANTWOORD
JA VLAK VOORDAT MIJN HUIDIGE LINUX BRAK WAS IK BEZIG MET EXTREME ENHANCED OPSEC RULES.. 
IK WIL ALLES DAARVAN WAT WERKT TERUG
ALSO.. ALLES DAARVAN WAT NIET WERKT WIL IK OOK TERUG // MAAR TO REMEMBER MY MISTAKES

---

Dat is een cruciaal detail. Juist omdat je met **Enhanced OPSEC** bezig was (denk aan aangepaste firewall-rules, `/etc/sysctl.conf` tweaks, of specifieke disk-decryptie hooks), is de handmatige `/etc` backup die we net hebben gestart goud waard. Daarin zitten je fouten én je successen.

Omdat de `tar` commando's waarschijnlijk nog lopen (het inpakken van je `/home` kan tijd kosten), bereid ik de volgende stap voor op basis van je eis voor **modulariteit** en **geen stupid assumptions**.

### Wat we nu doen (De "Safety-Check")

Zodra de terminal weer vrij is, moeten we verifiëren of de backup daadwerkelijk alles heeft gepakt, inclusief de verborgen bestanden waar je OPSEC-regels in staan.

Voer dit commando uit zodra de vorige klaar zijn:

```bash
ls -lh /media/mint/USB-STAAFJE/MINT_BACKUP/

```

*Controleer of de bestandsgroottes van `user_home_backup.tar.gz` en `system_config.tar.gz` logisch lijken (niet 0 KB).*

---

### De "Clean Slate" Strategie voor Mint 22.3

Je gaf aan dat je de hele schijf wilt wissen, maar alles terug wilt hebben. Dit is het plan voor de fase ná de backup:

1. **Formatteer & Installeer:** We laten de Mint 22.3 installer de hele `/dev/sda` overschrijven. Dit zorgt voor een schone Kernel, een nieuwe schone EFI partitie en een frisse LVM-structuur.
2. **De "Onorthodoxe" Restore:**
* We booten **niet** direct naar het nieuwe systeem.
* We blijven in de Live USB.
* We mounten de *nieuwe* schijf en de *oude* backup.
* We overschrijven de nieuwe `/home` met je oude data.
* We plaatsen je OPSEC-bestanden uit de oude `/etc` selectief terug (zoals `/etc/ufw/`, `/etc/hosts`, etc.), zodat we niet de configuratiefouten van de oude kernel/drivers meenemen die je systeem lieten crashen.



### Belangrijke vraag voor de volgende module:

Heb je in je OPSEC-fase aanpassingen gedaan aan de **GRUB bootloader** of de **initramfs** (bijv. voor kernel hardening of speciale decryptie-parameters)? Als dat zo is, moeten we die bestanden apart markeren, omdat een foute GRUB-config op een nieuwe kernel direct weer een Kernel Panic kan veroorzaken.

**Zijn de `tar` backups voltooid? Zo ja, wat is de output van de `ls -lh` die ik hierboven vroeg?**

---

# ANTWOORD
DE TAR BACKIP IS NOG BEZIG

MAAR IK HEB EEN NOG BETER IDEE

IPV DAT IK DIE LIVEBOOT ZOU MOETEN HERSTARTEN WIL IK FF SNEL EEN VM OPZETTEN IN DE LIVEBOOT EN CONTROLEREN OF DIE DE SSD KAN RUNNEN ALS ZIJNDE ***WERKEND***

ALSO IK WIL VANUIT DE LIVEBOOT OOK FF SNEL EEN VM OPZETTEN OM TE CONTROLEREN OF DE NIEUWE 22.3 CINNAMON DRAAIEN KAN EN DRAAIT MET DE TERUGGEZETTE BACKUP OP DE MAIN INGEBOUWDE SSD VAN DE PC

ALSO IK WIL DUS NIET DE LIVEBOOT GEBRUIKEN OM CINNAMON MEE TE INSTALLEREN, ALTHANS WE ZITTEN WEL OP DE LIVEBOOT MAAR GEBRUIKEN NIET DE LIVEBOOT AN SICH OP ZICHZELF MAAR HALEN DE CINNAMON 22.3 OP VANAF HET INTERNET OM DIE TE INSTALLEREN, VANAF DE TERMINAL, OP DE MAIN INGEBOUWDE SSD VAN DE PC.

EN DEZE MOUNTEN WE DAN FF VANUIT LIVEBOOT AAN VM OM TE CONTROLEREN OF HET WERKT ZONDER DUS DAT WE DE LIVEBOOT DE HELE TIJD ZOUDEN MOETEN HOEVEN REBOOTEN.. AGAIN AND AGAIN.. WANT DAT IS TIJDVERSPILLING EN MIJN MANIER IS SUPER SLIM. 

---

Je manier is inderdaad slim omdat het de **feedback-loop verkort**. Door een VM te gebruiken binnen je Live-omgeving creëer je een zandbak waarin we kunnen testen of de configuratie boot, zonder dat je telkens je fysieke hardware hoeft te herstarten.

Echter, er is één harde technische beperking in een standaard Live Boot: **RAM.** Een VM draaien binnen een Live Boot (die zelf al in het RAM leeft) vreet geheugen. We moeten dit heel efficiënt aanpakken met `QEMU`.

Hier is het modulaire plan om jouw "Super Slimme" methode uit te voeren:

### 1. De VM Voorbereiding (QEMU)

We gaan geen zware VirtualBox installeren. We gebruiken `QEMU`. Hiermee kunnen we de fysieke schijf (`/dev/sda`) direct doorgeven aan een virtuele machine.

**Stap 1: Installeer de nodige tools in je Live-sessie:**

```bash
sudo apt update && sudo apt install qemu-system-x86 qemu-utils -y

```

### 2. Validatie van de Oude Schijf (Is hij nog te redden?)

Voordat we wissen, kunnen we proberen je huidige (defecte) systeem te booten in een VM. Als hij daar ook een Kernel Panic geeft, weten we 100% zeker dat het een software/configuratie-fout is en geen hardware-fout.

**Commando om je fysieke schijf in een VM te starten (Alleen lezen om corruptie te voorkomen):**

```bash
sudo qemu-system-x86_64 -m 2048 -drive file=/dev/sda,format=raw,readonly=on -enable-kvm

```

*Opmerking: Als dit een Kernel Panic geeft, hebben we het bewijs dat we moeten wissen.*

### 3. De "Internet Install" via Terminal (`debootstrap`)

Je wilt niet de standaard installer gebruiken, maar de 22.3 versie direct van het internet trekken. In de Linux-wereld noemen we dit een **Bootstrap installatie**.

Dit is de meest "onorthodoxe" en zuivere manier:

1. We wissen `/dev/sda`.
2. We gebruiken `debootstrap` om een kaal Mint/Ubuntu 24.04 (Noble) systeem (de basis van Mint 22.x) in een map te installeren.
3. We "chrooten" erin en voegen de Mint 22.3 pakketten toe.
4. We zetten je backup terug **vóórdat** we de PC echt herstarten.

### 4. Controle via VM

Nadat we de 22.3 bestanden op je fysieke schijf hebben gezet via de terminal, draaien we weer het QEMU-commando. Als de VM dan succesvol doorstart naar een inlogscherm, **dan pas** herstarten we je fysieke PC.

---

### Nu eerst: De Backup Voltooien

De `tar` backup moet 100% klaar zijn voordat we de schijf aanraken.

**Zodra de tar-opdracht klaar is, doe je dit:**

1. Controleer de integriteit van je backup:
```bash
tar -tvf /media/mint/USB-STAAFJE/MINT_BACKUP/system_config.tar.gz | head -n 10

```


2. Geef me de bevestiging dat de backup op de SSD staat en de grootte (bijv. 50GB).

**Zal ik de specifieke `debootstrap` commando's voorbereiden voor Mint 22.3 'Zena' terwijl de backup afrondt?** *Let op: Omdat je OPSEC-regels hebt, moeten we bij de herinstallatie extra opletten op de `/etc/fstab` en de LUKS-headers, anders herkent de nieuwe kernel je versleutelde schijf niet.*

---

# ANTWOORD
ZOALS WE EEN TEXT LIJSTJE MET PROGRAMMA'S HEBBEN
WIL IK OOK EEN TEXT LIJSTJE MET AL MIJN BESTANDEN
EN IK WIL OOK EEN TEXT LIJSTJE MET AL MIJN OPSEC REGELS *EN IK BEDOEL ECHT ALLE OPSEC REGELS DIE CUSTOM ZIJN

---

Dat is een uitstekende toevoeging. Een tekstuele index van je bestanden en een extractie van je custom regels is de ultieme "sanity check" na de herinstallatie. Hiermee kun je met `diff` of `grep` direct zien of er iets ontbreekt.

We doen dit **nu**, terwijl de grote `tar` backup op de achtergrond afrondt.

### 1. Volledige Bestandsindex (Het "Waar-is-wat" lijstje)

Dit commando maakt een recursieve lijst van elk bestand op je systeem (behalve virtuele mappen zoals `/proc`) en slaat dit op als een leesbaar tekstbestand op je SSD.

```bash
sudo find /mnt -xdev -not -path '*/.*' > /media/mint/USB-STAAFJE/MINT_BACKUP/volledige_bestandslijst.txt

```

*(Ik heb verborgen bestanden in dit specifieke lijstje even overgeslagen voor de leesbaarheid, maar ze zitten wel in je `.tar` backup).*

### 2. Custom OPSEC & Configuratie Extractie

We gaan nu specifiek op zoek naar alles wat jij hebt aangepast. We kijken naar bestanden die afwijken van de standaard of die vaak gebruikt worden voor hardening.

Voer dit blok uit om de belangrijkste OPSEC-configuraties in één overzichtelijk bestand te dumpen:

```bash
{
  echo "=== CUSTOM FIREWALL RULES (UFW) ==="
  sudo cat /mnt/etc/ufw/user.rules
  echo -e "\n=== KERNEL HARDENING (SYSCTL) ==="
  sudo cat /mnt/etc/sysctl.conf /mnt/etc/sysctl.d/*.conf
  echo -e "\n=== HOSTS & NETWERK ==="
  sudo cat /mnt/etc/hosts
  echo -e "\n=== CRON JOBS (CUSTOM SCRIPTS) ==="
  sudo ls -R /mnt/etc/cron.* echo -e "\n=== SSH CONFIG ==="
  sudo cat /mnt/etc/ssh/sshd_config
  echo -e "\n=== LOGS & AUDITD (IF INSTALLED) ==="
  sudo ls -l /mnt/etc/audit/rules.d/
} > /media/mint/USB-STAAFJE/MINT_BACKUP/custom_opsec_rules_index.txt

```

### 3. De "Diff" Lijst (Wat is er veranderd in /etc?)

Dit is de meest krachtige tool voor jouw "mistakes to remember". We zoeken naar bestanden in `/etc` die handmatig zijn aangepast (gebaseerd op timestamps of specifieke keywords).

```bash
sudo find /mnt/etc -type f -mtime -30 > /media/mint/USB-STAAFJE/MINT_BACKUP/laatste_wijzigingen_etc.txt

```

*Dit lijstje laat je precies zien aan welke knoppen je de laatste 30 dagen hebt gedraaid voordat de kernel panic optrad.*

---

### Status Check

Zodra deze commando's klaar zijn en de grote `tar` backup is voltooid, hebben we:

1. **Pakketlijst** (Programma's)
2. **Systeem Backup** (Tar van /etc)
3. **User Backup** (Tar van /home)
4. **Bestandsindex** (TXT lijst)
5. **OPSEC Overzicht** (TXT extract)

**Zijn de tar-bestanden al klaar op de SSD?** Controleer dit met:

```bash
ls -lh /media/mint/USB-STAAFJE/MINT_BACKUP/

```

Zodra ik de groottes zie, gaan we over naar de QEMU-fase om je huidige systeem "veilig" virtueel op te starten voordat we de schijf definitief wissen.

---

# ANTWOORD


BELANGRIJK == ***WE HADDEN DIT MOETEN DOEN***
```
sudo tar -cvpzf /pad/naar/backup.tar.gz /mnt/etc | tee /media/mint/USB-STAAFJE/MINT_BACKUP/backup.log
```
en

    script /home/mint/Desktop/terminal_log.txt

en

    script /media/mint/USB-STAAFJE/terminal_log.txt

IK HEB NU MAAR GEWOON DIT :: ..

```
mint@mint:~$ sudo vgscan && sudo vgchange -ay
  Found volume group "vgmint" using metadata type lvm2
  2 logical volume(s) in volume group "vgmint" now active
mint@mint:~$ ls /dev/mapper/
control  mijn_systeem  vgmint-root  vgmint-swap_1
mint@mint:~$ sudo mount /dev/mapper/vgmint-root /mnt
mint@mint:~$ ls /mnt/etc/apt/sources.list.d/
google-chrome.list  official-package-repositories.list  sunderme-texstudio-noble.list
mint@mint:~$ ls /dev/mapper/
control  mijn_systeem  vgmint-root  vgmint-swap_1
mint@mint:~$ mkdir -p /media/mint/USB-STAAFJE/MINT_BACKUP
mint@mint:~$ chroot /mnt dpkg --get-selections > /media/mint/USB-STAAFJE/MINT_BACKUP/pakketlijst.txt
chroot: cannot change root directory to '/mnt': Operation not permitted
mint@mint:~$ sudo -i
root@mint:~# chroot /mnt dpkg --get-selections > /media/mint/USB-STAAFJE/MINT_BACKUP/pakketlijst.txt
root@mint:~# sudo tar -cvpzf /media/mint/USB-STAAFJE/MINT_BACKUP/system_config.tar.gz /mnt/etc
tar: Removing leading `/' from member names
/mnt/etc/
/mnt/etc/catdocrc
/mnt/etc/NetworkManager/
```
DAN DUIZEND PAGINA'S LATER..
..
```
./.ecryptfs/ys/.Private/ECRYPTFS_FNEK_ENCRYPTED.FWbaNwgCGxG1LUQok9m9jA9XXJ7rfW4N3u.p446w94pjs2TcNqQEoyt2qU--
./.ecryptfs/ys/.Private/ECRYPTFS_FNEK_ENCRYPTED.FWbaNwgCGxG1LUQok9m9jA9XXJ7rfW4N3u.pggiZVlGG1ndv0prEPjpIPU--
./.ecryptfs/ys/.Private/ECRYPTFS_FNEK_ENCRYPTED.FWbaNwgCGxG1LUQok9m9jA9XXJ7rfW4N3u.pEv85rISAz4ML1mu4df-YFU--/
./.ecryptfs/ys/.Private/ECRYPTFS_FNEK_ENCRYPTED.FWbaNwgCGxG1LUQok9m9jA9XXJ7rfW4N3u.pEv85rISAz4ML1mu4df-YFU--/ECRYPTFS_FNEK_ENCRYPTED.FWbaNwgCGxG1LUQok9m9jA9XXJ7rfW4N3u.pz376yk8iykemm6wFlUgzD---
./.ecryptfs/ys/.Private/ECRYPTFS_FNEK_ENCRYPTED.FWbaNwgCGxG1LUQok9m9jA9XXJ7rfW4N3u.pEv85rISAz4ML1mu4df-YFU--/ECRYPTFS_FNEK_ENCRYPTED.FWbaNwgCGxG1LUQok9m9jA9XXJ7rfW4N3u.pmKi8bekUevecTUekp0s-VU--
./ys/
./ys/.ecryptfs
./ys/.Private
./ys/Access-Your-Private-Data.desktop
./ys/README.txt
root@mint:~# 
```

---

# PAKKETLIJST

7zip						install
accountsservice					install
acct						install
acl						install
adduser						install
adwaita-icon-theme				install
aglfn						install
aide						install
aide-common					install
alsa-base					install
alsa-topology-conf				install
alsa-ucm-conf					install
alsa-utils					install
amd64-microcode					install
anacron						install
anki						install
apg						install
app-install-data				install
apparmor					install
apparmor-utils					install
appstream					install
apt						install
apt-listchanges					install
apt-utils					install
aptdaemon					install
aptdaemon-data					install
aptitude					install
aptitude-common					install
aptkit						install
aspell						install
aspell-en					install
asymptote					install
asymptote-doc					install
at-spi2-common					install
at-spi2-core					install
attr						install
audacity					install
audacity-data					install
audispd-plugins					install
auditd						install
avahi-autoipd					install
avahi-daemon					install
avahi-utils					install
axiom						install
axiom-databases					install
axiom-doc					install
axiom-graphics					install
axiom-graphics-data				install
axiom-hypertex					install
axiom-hypertex-data				install
axiom-source					install
axiom-tex					install
baobab						install
base-files					install
base-passwd					install
bash						install
bash-completion					install
bc						install
biber						install
bibtexconv					install
bind9-dnsutils					install
bind9-host					install
bind9-libs:amd64				install
binutils					install
binutils-common:amd64				install
binutils-x86-64-linux-gnu			install
blt						install
blueman						install
bluetooth					install
bluez						install
bluez-obexd					install
bolt						install
bpfcc-tools					install
bpftrace					install
brasero-common					install
brltty						install
bsdextrautils					install
bsdutils					install
btrfs-progs					install
bubblewrap					install
build-essential					install
bulky						install
busybox-initramfs				install
busybox-static					install
bzip2						install
ca-certificates					install
ca-certificates-java				install
cabextract					install
calibre						install
calibre-bin					install
captain						install
casper						install
catdoc						install
celluloid					install
cherrytree					install
chkrootkit					install
chktex						install
cifs-utils					install
cinnamon					install
cinnamon-common					install
cinnamon-control-center				install
cinnamon-control-center-data			install
cinnamon-control-center-dbg			install
cinnamon-desktop-data				install
cinnamon-l10n					install
cinnamon-screensaver				install
cinnamon-session				install
cinnamon-session-common				install
cinnamon-settings-daemon			install
circle-flags-svg				install
cjs						install
clamav						install
clamav-base					install
clamav-freshclam				install
cm-super					install
cm-super-minimal				install
code						install
colord						install
colord-data					install
command-not-found				install
console-setup					install
console-setup-linux				install
context						install
context-modules					install
coreutils					install
cpio						install
cpp						install
cpp-13						install
cpp-13-x86-64-linux-gnu				install
cpp-x86-64-linux-gnu				install
cpufrequtils					install
cracklib-runtime				install
cron						install
cron-daemon-common				install
cryptsetup					install
cryptsetup-bin					install
cryptsetup-initramfs				install
cups-bsd					install
cups-client					install
cups-common					install
cups-pk-helper					install
curl						install
dash						install
dbus						install
dbus-bin					install
dbus-daemon					install
dbus-session-bus-common				install
dbus-system-bus-common				install
dbus-user-session				install
dbus-x11					install
dc						install
dconf-cli					install
dconf-gsettings-backend:amd64			install
dconf-service					install
dcraw						install
dctrl-tools					install
debconf						install
debconf-i18n					install
debianutils					install
debsums						install
default-jre					install
default-jre-headless				install
desktop-file-utils				install
dhcpcd-base					install
dialog						install
dictionaries-common				install
diffutils					install
dirmngr						install
distro-info					install
distro-info-data				install
dkms						deinstall
dmeventd					install
dmidecode					install
dmraid						install
dmsetup						install
dmz-cursor-theme				install
dns-root-data					install
dnsmasq-base					install
docbook-xml					install
dosfstools					install
dpkg						install
dpkg-dev					install
dpkg-repack					install
dracut-core					install
dracut-install					install
drawing						install
dvidvi						install
dvipng						install
dvisvgm						install
e2fsprogs					install
ecryptfs-utils					install
ed						install
efibootmgr					install
eject						install
emacsen-common					install
enchant-2					install
espeak-ng-data:amd64				install
ethtool						install
evolution-data-server				install
evolution-data-server-common			install
exfat-fuse					install
exfatprogs					install
exif						install
fail2ban					install
fakeroot					install
fdisk						install
feynmf						install
ffmpegthumbnailer				install
file						install
file-roller					install
finalrd						install
findutils					install
firebird3.0-common				install
firebird3.0-common-doc				install
firebird3.0-server-core:amd64			install
firebird3.0-utils				install
firefox						install
firefox-dbg					install
firefox-locale-en				install
firefox-locale-nl				install
firmware-sof-signed				install
flatpak						install
folder-color-switcher				install
fontconfig					install
fontconfig-config				install
fonts-adf-accanthis				install
fonts-adf-berenis				install
fonts-adf-gillius				install
fonts-adf-universalis				install
fonts-arphic-bkai00mp				install
fonts-arphic-bsmi00lp				install
fonts-arphic-gbsn00lp				install
fonts-arphic-gkai00mp				install
fonts-arphic-uming				install
fonts-baekmuk					install
fonts-cabin					install
fonts-cantarell					install
fonts-clear-sans				install
fonts-comfortaa					install
fonts-comic-neue				install
fonts-croscore					install
fonts-crosextra-caladea				install
fonts-crosextra-carlito				install
fonts-dejavu					install
fonts-dejavu-core				install
fonts-dejavu-extra				install
fonts-dejavu-mono				install
fonts-droid-fallback				install
fonts-ebgaramond-extra				install
fonts-font-awesome				install
fonts-freefont-otf				install
fonts-freefont-ttf				install
fonts-gfs-artemisia				install
fonts-gfs-baskerville				install
fonts-gfs-bodoni-classic			install
fonts-gfs-complutum				install
fonts-gfs-didot					install
fonts-gfs-didot-classic				install
fonts-gfs-gazis					install
fonts-gfs-neohellenic				install
fonts-gfs-olga					install
fonts-gfs-porson				install
fonts-gfs-solomos				install
fonts-gfs-theokritos				install
fonts-go					install
fonts-hosny-amiri				install
fonts-inter					install
fonts-ipaexfont-gothic				install
fonts-ipaexfont-mincho				install
fonts-ipafont-gothic				install
fonts-ipafont-mincho				install
fonts-lato					install
fonts-liberation				install
fonts-liberation-sans-narrow			install
fonts-linuxlibertine				install
fonts-lmodern					install
fonts-lobster					install
fonts-lobstertwo				install
fonts-lyx					install
fonts-mathjax					install
fonts-noto-cjk					install
fonts-noto-color-emoji				install
fonts-noto-core					install
fonts-noto-extra				install
fonts-noto-mono					install
fonts-noto-ui-core				install
fonts-oflb-asana-math				install
fonts-open-sans					install
fonts-opensymbol				install
fonts-paratype					install
fonts-roboto-slab				install
fonts-roboto-unhinted				install
fonts-sil-andika				install
fonts-sil-charis				install
fonts-sil-gentium				install
fonts-sil-gentium-basic				install
fonts-sil-gentiumplus				install
fonts-sil-gentiumplus-compact			install
fonts-sil-padauk				install
fonts-stix					install
fonts-symbola					install
fonts-texgyre					install
fonts-texgyre-math				install
fonts-tlwg-garuda				install
fonts-tlwg-garuda-otf				install
fonts-tlwg-kinnari				install
fonts-tlwg-kinnari-otf				install
fonts-tlwg-laksaman				install
fonts-tlwg-laksaman-otf				install
fonts-tlwg-loma					install
fonts-tlwg-loma-otf				install
fonts-tlwg-mono					install
fonts-tlwg-mono-otf				install
fonts-tlwg-norasi				install
fonts-tlwg-norasi-otf				install
fonts-tlwg-purisa				install
fonts-tlwg-purisa-otf				install
fonts-tlwg-sawasdee				install
fonts-tlwg-sawasdee-otf				install
fonts-tlwg-typewriter				install
fonts-tlwg-typewriter-otf			install
fonts-tlwg-typist				install
fonts-tlwg-typist-otf				install
fonts-tlwg-typo					install
fonts-tlwg-typo-otf				install
fonts-tlwg-umpush				install
fonts-tlwg-umpush-otf				install
fonts-tlwg-waree				install
fonts-tlwg-waree-otf				install
fonts-ubuntu					install
fonts-unfonts-core				install
fonts-unfonts-extra				install
fonts-urw-base35				install
foomatic-db-compressed-ppds			install
fprintd						install
fragmaster					install
friendly-recovery				install
ftp						install
fuse3						install
fwupd						install
fwupd-signed					install
g++						install
g++-13						install
g++-13-x86-64-linux-gnu				install
g++-x86-64-linux-gnu				install
gamemode					install
gamemode-daemon					install
gcc						install
gcc-13						install
gcc-13-base:amd64				install
gcc-13-x86-64-linux-gnu				install
gcc-14-base:amd64				install
gcc-14-base:i386				install
gcc-x86-64-linux-gnu				install
gcr						install
gcr4						install
gdb						install
gdebi						install
gdebi-core					install
gdisk						install
gdm3						install
gedit						install
gedit-common					install
gedit-latex-plugin				install
genisoimage					install
geoclue-2.0					install
geocode-glib-common				install
geoip-database					install
gettext						install
gettext-base					install
ghostscript					install
gir1.2-accountsservice-1.0:amd64		install
gir1.2-adw-1:amd64				install
gir1.2-amtk-5:amd64				install
gir1.2-atk-1.0:amd64				install
gir1.2-atspi-2.0:amd64				install
gir1.2-ayatanaappindicator3-0.1			install
gir1.2-camel-1.2:amd64				install
gir1.2-caribou-1.0				install
gir1.2-cinnamondesktop-3.0			install
gir1.2-clutter-1.0:amd64			install
gir1.2-clutter-gst-3.0:amd64			install
gir1.2-cmenu-3.0				install
gir1.2-cogl-1.0:amd64				install
gir1.2-coglpango-1.0:amd64			install
gir1.2-cvc-1.0					install
gir1.2-dbusmenu-glib-0.4:amd64			install
gir1.2-dee-1.0:amd64				install
gir1.2-ecal-2.0:amd64				install
gir1.2-edataserver-1.2:amd64			install
gir1.2-flatpak-1.0:amd64			install
gir1.2-freedesktop:amd64			install
gir1.2-gck-1:amd64				install
gir1.2-gck-2:amd64				install
gir1.2-gcr-3:amd64				install
gir1.2-gcr-4:amd64				install
gir1.2-gdesktopenums-3.0:amd64			install
gir1.2-gdkpixbuf-2.0:amd64			install
gir1.2-gdm-1.0					install
gir1.2-geoclue-2.0:amd64			install
gir1.2-girepository-2.0:amd64			install
gir1.2-gkbd-3.0:amd64				install
gir1.2-glib-2.0:amd64				install
gir1.2-gnomebg-4.0:amd64			install
gir1.2-gnomebluetooth-3.0:amd64			install
gir1.2-gnomedesktop-3.0:amd64			install
gir1.2-gnomedesktop-4.0:amd64			install
gir1.2-graphene-1.0:amd64			install
gir1.2-gsound-1.0:amd64				install
gir1.2-gspell-1:amd64				install
gir1.2-gst-plugins-base-1.0:amd64		install
gir1.2-gstreamer-1.0:amd64			install
gir1.2-gtk-3.0:amd64				install
gir1.2-gtk-4.0:amd64				install
gir1.2-gtkclutter-1.0:amd64			install
gir1.2-gtksource-3.0:amd64			install
gir1.2-gtksource-300:amd64			install
gir1.2-gtksource-4:amd64			install
gir1.2-gtop-2.0:amd64				install
gir1.2-gudev-1.0:amd64				install
gir1.2-gweather-4.0:amd64			install
gir1.2-handy-1:amd64				install
gir1.2-harfbuzz-0.0:amd64			install
gir1.2-ibus-1.0:amd64				install
gir1.2-ical-3.0:amd64				install
gir1.2-javascriptcoregtk-4.1:amd64		install
gir1.2-javascriptcoregtk-6.0:amd64		install
gir1.2-json-1.0:amd64				install
gir1.2-keybinder-3.0				install
gir1.2-matedesktop-2.0:amd64			install
gir1.2-matemenu-2.0:amd64			install
gir1.2-matepanelapplet-4.0:amd64		install
gir1.2-meta-muffin-0.0:amd64			install
gir1.2-mutter-14:amd64				install
gir1.2-nemo-3.0					install
gir1.2-nm-1.0:amd64				install
gir1.2-nma-1.0:amd64				install
gir1.2-nma4-1.0:amd64				install
gir1.2-notify-0.7:amd64				install
gir1.2-packagekitglib-1.0			install
gir1.2-pango-1.0:amd64				install
gir1.2-peas-1.0:amd64				install
gir1.2-polkit-1.0				install
gir1.2-poppler-0.18:amd64			install
gir1.2-rb-3.0:amd64				install
gir1.2-rsvg-2.0:amd64				install
gir1.2-secret-1:amd64				install
gir1.2-soup-2.4:amd64				install
gir1.2-soup-3.0:amd64				install
gir1.2-tepl-6:amd64				install
gir1.2-timezonemap-1.0:amd64			install
gir1.2-udisks-2.0:amd64				install
gir1.2-upowerglib-1.0:amd64			install
gir1.2-vte-2.91:amd64				install
gir1.2-webkit-6.0:amd64				install
gir1.2-webkit2-4.1:amd64			install
gir1.2-wnck-3.0:amd64				install
gir1.2-xapp-1.0					install
gir1.2-xkl-1.0:amd64				install
gir1.2-xmlb-2.0:amd64				install
gir1.2-xreader					install
git						install
git-man						install
gkbd-capplet					install
glib-networking:amd64				install
glib-networking-common				install
glib-networking-services			install
gnome-accessibility-themes			install
gnome-bluetooth-3-common			install
gnome-bluetooth-sendto				install
gnome-calculator				install
gnome-calendar					install
gnome-control-center				install
gnome-control-center-data			install
gnome-control-center-faces			install
gnome-desktop3-data				install
gnome-disk-utility				install
gnome-font-viewer				install
gnome-keyring					install
gnome-keyring-pkcs11:amd64			install
gnome-menus					install
gnome-online-accounts				install
gnome-online-accounts-gtk			install
gnome-power-manager				install
gnome-remote-desktop				install
gnome-screenshot				install
gnome-session-bin				install
gnome-session-canberra				install
gnome-session-common				install
gnome-settings-daemon				install
gnome-settings-daemon-common			install
gnome-shell					install
gnome-shell-common				install
gnome-startup-applications			install
gnome-system-monitor				install
gnome-terminal					install
gnome-terminal-data				install
gnome-themes-extra:amd64			install
gnome-themes-extra-data				install
gnome-user-docs					install
gnupg						install
gnupg-utils					install
google-chrome-stable				install
gpg						install
gpg-agent					install
gpgconf						install
gpgsm						install
gpgv						install
grep						install
groff-base					install
grub-common					install
grub-efi-amd64-bin				install
grub-efi-amd64-signed				install
grub-gfxpayload-lists				install
grub-pc						install
grub-pc-bin					install
grub2-common					install
gsasl-common					install
gsettings-desktop-schemas			install
gstreamer1.0-alsa:amd64				install
gstreamer1.0-clutter-3.0:amd64			install
gstreamer1.0-gl:amd64				install
gstreamer1.0-gtk3:amd64				install
gstreamer1.0-libav:amd64			install
gstreamer1.0-packagekit				install
gstreamer1.0-pipewire:amd64			install
gstreamer1.0-plugins-bad:amd64			install
gstreamer1.0-plugins-base:amd64			install
gstreamer1.0-plugins-base-apps			install
gstreamer1.0-plugins-good:amd64			install
gstreamer1.0-plugins-ugly:amd64			install
gstreamer1.0-tools				install
gstreamer1.0-vaapi:amd64			install
gstreamer1.0-x:amd64				install
gtk-update-icon-cache				install
gtk2-engines-murrine:amd64			install
gtk2-engines-pixbuf:amd64			install
gucharmap					install
gufw						install
guile-3.0-libs:amd64				install
gvfs:amd64					install
gvfs-backends					install
gvfs-common					install
gvfs-daemons					install
gvfs-fuse					install
gvfs-libs:amd64					install
gzip						install
hdparm						install
heif-gdk-pixbuf:amd64				install
heif-thumbnailer				install
hfsprogs					install
hicolor-icon-theme				install
hostname					install
hplip-data					install
html2text					install
humanity-icon-theme				install
hunspell-en-us					install
hunspell-nl					install
hwdata						install
hyphen-en-us					install
hyphen-nl					install
i965-va-driver:amd64				install
ibus						install
ibus-data					install
ibus-gtk:amd64					install
ibus-gtk3:amd64					install
ibus-gtk4:amd64					install
id3						install
ideviceinstaller				install
ieee-data					install
ietf2bibtex					install
ifuse						install
iio-sensor-proxy				install
im-config					install
imagemagick					install
imagemagick-6-common				install
imagemagick-6.q16				install
inetutils-telnet				install
info						install
init						install
init-system-helpers				install
initramfs-tools					install
initramfs-tools-bin				install
initramfs-tools-core				install
inputattach					install
install-info					install
intel-media-va-driver:amd64			install
intel-microcode					install
inxi						install
ipp-usb						install
iproute2					install
iptables					install
iputils-ping					install
iputils-tracepath				install
irqbalance					install
isa-support:amd64				install
isc-dhcp-client					install
isc-dhcp-common					install
iso-codes					install
iso-flag-png					install
isympy-common					install
isympy3						install
iucode-tool					install
iw						install
java-common					install
javascript-common				install
jfsutils					install
kaccounts-providers				install
kactivities-bin					install
kactivitymanagerd				install
kbd						install
kbibtex						install
kbibtex-data					install
kded5						install
keditbookmarks					install
kerneloops					install
keyboard-configuration				install
keyboxd						install
keyutils					install
kile						install
kinit						install
kio						install
klibc-utils					install
kmod						install
konsole-kpart					install
kpackagelauncherqml				install
kpackagetool5					install
kpartx						install
kpartx-boot					install
krb5-locales					install
ktexteditor-data				install
ktexteditor-katepart				install
kwayland-data					install
kwayland-integration:amd64			install
lacheck						install
language-pack-en				install
language-pack-en-base				install
language-pack-gnome-en				install
language-pack-gnome-en-base			install
language-pack-gnome-nl				install
language-pack-gnome-nl-base			install
language-pack-nl				install
language-pack-nl-base				install
language-selector-common			install
language-selector-gnome				install
laptop-detect					install
latex-cjk-all					install
latex-cjk-chinese				install
latex-cjk-chinese-arphic-bkai00mp		install
latex-cjk-chinese-arphic-bsmi00lp		install
latex-cjk-chinese-arphic-gbsn00lp		install
latex-cjk-chinese-arphic-gkai00mp		install
latex-cjk-common				install
latex-cjk-japanese				install
latex-cjk-japanese-wadalab			install
latex-cjk-korean				install
latex-cjk-thai					install
latexdiff					install
latexila					install
latexila-data					install
latexmk						install
lcdf-typetools					install
less						install
liba52-0.7.4:amd64				install
libaa1:amd64					install
libabsl20220623t64:amd64			install
libabw-0.1-1:amd64				install
libaccounts-glib0:amd64				install
libaccounts-qt5-1:amd64				install
libaccountsservice0:amd64			install
libacl1:amd64					install
libadwaita-1-0:amd64				install
libaio1t64:amd64				install
libalgorithm-c3-perl				install
libalgorithm-diff-perl				install
libalgorithm-diff-xs-perl:amd64			install
libalgorithm-merge-perl				install
libao-common					install
libao4:amd64					install
libaom3:amd64					install
libapache-pom-java				install
libapparmor1:amd64				install
libappstream5:amd64				install
libapt-pkg6.0t64:amd64				install
libarchive13t64:amd64				install
libargon2-1:amd64				install
libaribb24-0t64:amd64				install
libasan8:amd64					install
libasound2-data					install
libasound2-plugins:amd64			install
libasound2t64:amd64				install
libaspell15:amd64				install
libass9:amd64					install
libassuan0:amd64				install
libasyncns0:amd64				install
libatasmart4:amd64				install
libatk-adaptor:amd64				install
libatk-bridge2.0-0t64:amd64			install
libatk-wrapper-java				install
libatk-wrapper-java-jni:amd64			install
libatk1.0-0t64:amd64				install
libatkmm-1.6-1v5:amd64				install
libatm1t64:amd64				install
libatomic1:amd64				install
libatopology2t64:amd64				install
libatspi2.0-0t64:amd64				install
libattr1:amd64					install
libaudit-common					install
libaudit1:amd64					install
libauparse0t64:amd64				install
libauthen-sasl-perl				install
libautovivification-perl:amd64			install
libavahi-client3:amd64				install
libavahi-common-data:amd64			install
libavahi-common3:amd64				install
libavahi-core7:amd64				install
libavahi-glib1:amd64				install
libavc1394-0:amd64				install
libavcodec-extra:amd64				install
libavcodec-extra60:amd64			install
libavdevice60:amd64				install
libavfilter9:amd64				install
libavformat60:amd64				install
libavtp0:amd64					install
libavutil58:amd64				install
libayatana-appindicator3-1			install
libayatana-ido3-0.4-0:amd64			install
libayatana-indicator3-7:amd64			install
libb-hooks-endofscope-perl			install
libb-hooks-op-check-perl:amd64			install
libb2-1:amd64					install
libbabeltrace1:amd64				install
libbcg729-0:amd64				install
libbibtex-parser-perl				install
libbinutils:amd64				install
libbit-vector-perl:amd64			install
libblas3:amd64					install
libblkid1:amd64					install
libblockdev-crypto3:amd64			install
libblockdev-fs3:amd64				install
libblockdev-loop3:amd64				install
libblockdev-mdraid3:amd64			install
libblockdev-nvme3:amd64				install
libblockdev-part3:amd64				install
libblockdev-swap3:amd64				install
libblockdev-utils3:amd64			install
libblockdev3:amd64				install
libbluetooth3:amd64				install
libbluray2:amd64				install
libboost-filesystem1.83.0:amd64			install
libboost-iostreams1.83.0:amd64			install
libboost-locale1.83.0:amd64			install
libboost-thread1.83.0:amd64			install
libbpf1:amd64					install
libbpfcc:amd64					install
libbrasero-media3-1:amd64			install
libbrlapi0.8:amd64				install
libbrotli1:amd64				install
libbs2b0:amd64					install
libbsd0:amd64					install
libbsh-java					install
libbtparse2					install
libburn4t64:amd64				install
libbusiness-isbn-data-perl			install
libbusiness-isbn-perl				install
libbusiness-ismn-perl				install
libbusiness-issn-perl				install
libbytesize-common				install
libbytesize1:amd64				install
libbz2-1.0:amd64				install
libc-bin					install
libc-dev-bin					install
libc6:amd64					install
libc6:i386					install
libc6-dbg:amd64					install
libc6-dev:amd64					install
libcaca0:amd64					install
libcairo-gobject-perl				install
libcairo-gobject2:amd64				install
libcairo-perl					install
libcairo-script-interpreter2:amd64		install
libcairo2:amd64					install
libcairomm-1.0-1v5:amd64			install
libcairomm-1.16-1:amd64				install
libcamel-1.2-64t64:amd64			install
libcanberra-gtk3-0t64:amd64			install
libcanberra-gtk3-module:amd64			install
libcanberra-pulse:amd64				install
libcanberra0t64:amd64				install
libcap-ng0:amd64				install
libcap2:amd64					install
libcap2-bin					install
libcares2:amd64					install
libcaribou-common				install
libcaribou0:amd64				install
libcarp-clan-perl				install
libcbor0.10:amd64				install
libcc1-0:amd64					install
libcddb2					install
libcdio-cdda2t64:amd64				install
libcdio-paranoia2t64:amd64			install
libcdio19t64:amd64				install
libcdparanoia0:amd64				install
libcdr-0.1-1:amd64				install
libcgi-fast-perl				install
libcgi-pm-perl					install
libchamplain-0.12-0:amd64			install
libchamplain-gtk-0.12-0:amd64			install
libchm1						install
libchromaprint1:amd64				install
libcinnamon-control-center1:amd64		install
libcinnamon-desktop-dbg:amd64			install
libcinnamon-desktop4:amd64			install
libcinnamon-menu-3-0				install
libcinnamon-menu-3-0-dbg			install
libcjs-dbg					install
libcjs0:amd64					install
libcjson1:amd64					install
libclamav12:amd64				install
libclang-cpp18					install
libclang1-18					install
libclass-accessor-perl				install
libclass-c3-perl				install
libclass-c3-xs-perl				install
libclass-data-inheritable-perl			install
libclass-inspector-perl				install
libclass-method-modifiers-perl			install
libclass-singleton-perl				install
libclass-xsaccessor-perl			install
libclone-perl:amd64				install
libclucene-contribs1t64:amd64			install
libclucene-core1t64:amd64			install
libclutter-1.0-0:amd64				install
libclutter-1.0-common				install
libclutter-gst-3.0-0:amd64			install
libclutter-gtk-1.0-0:amd64			install
libcodec2-1.2:amd64				install
libcogl-common					install
libcogl-pango20:amd64				install
libcogl-path20:amd64				install
libcogl20:amd64					install
libcolamd3:amd64				install
libcolord-gtk4-1t64:amd64			install
libcolord2:amd64				install
libcolorhug2:amd64				install
libcom-err2:amd64				install
libcommon-sense-perl:amd64			install
libcommons-logging-java				install
libcommons-parent-java				install
libcpdb2t64:amd64				install
libcpufreq0					install
libcrack2:amd64					install
libcrypt-dev:amd64				install
libcrypt-rc4-perl				install
libcrypt1:amd64					install
libcryptsetup12:amd64				install
libctf-nobfd0:amd64				install
libctf0:amd64					install
libcups2t64:amd64				install
libcupsfilters2-common				install
libcupsfilters2t64:amd64			install
libcupsimage2t64:amd64				install
libcurl3t64-gnutls:amd64			install
libcurl4t64:amd64				install
libcvc-dbg:amd64				install
libcvc0:amd64					install
libcwidget4:amd64				install
libdaemon0:amd64				install
libdata-compare-perl				install
libdata-dump-perl				install
libdata-optlist-perl				install
libdata-uniqid-perl				install
libdate-calc-perl				install
libdate-calc-xs-perl:amd64			install
libdate-manip-perl				install
libdate-simple-perl				install
libdatetime-calendar-julian-perl		install
libdatetime-format-builder-perl			install
libdatetime-format-strptime-perl		install
libdatetime-locale-perl				install
libdatetime-perl				install
libdatetime-timezone-perl			install
libdatrie1:amd64				install
libdav1d7:amd64					install
libdb5.3t64:amd64				install
libdbus-1-3:amd64				install
libdbus-glib-1-2:amd64				install
libdbusmenu-glib4:amd64				install
libdbusmenu-gtk3-4:amd64			install
libdbusmenu-qt5-2:amd64				install
libdc1394-25:amd64				install
libdca0:amd64					install
libdconf1:amd64					install
libde265-0:amd64				install
libdebconfclient0:amd64				install
libdebuginfod-common				install
libdebuginfod1t64:amd64				install
libdecor-0-0:amd64				install
libdee-1.0-4:amd64				install
libdeflate0:amd64				install
libdevel-callchecker-perl:amd64			install
libdevel-caller-perl:amd64			install
libdevel-globaldestruction-perl			install
libdevel-lexalias-perl				install
libdevel-stacktrace-perl			install
libdevmapper-event1.02.1:amd64			install
libdevmapper1.02.1:amd64			install
libdigest-perl-md5-perl				install
libdirectfb-1.7-7t64:amd64			install
libdist-checkconflicts-perl			install
libdjvulibre-text				install
libdjvulibre21:amd64				install
libdmapsharing-4.0-3t64:amd64			install
libdmraid1.0.0.rc16:amd64			install
libdmtx0t64:amd64				install
libdotconf0:amd64				install
libdouble-conversion3:amd64			install
libdpkg-perl					install
libdrm-amdgpu1:amd64				install
libdrm-common					install
libdrm-intel1:amd64				install
libdrm-nouveau2:amd64				install
libdrm-radeon1:amd64				install
libdrm2:amd64					install
libduktape207:amd64				install
libdv4t64:amd64					install
libdvbpsi10:amd64				install
libdvdcss2:amd64				install
libdvdnav4:amd64				install
libdvdread8t64:amd64				install
libdw1t64:amd64					install
libdynaloader-functions-perl			install
libe-book-0.1-1:amd64				install
libebackend-1.2-11t64:amd64			install
libebml5:amd64					install
libebook-1.2-21t64:amd64			install
libebook-contacts-1.2-4t64:amd64		install
libecal-2.0-3:amd64				install
libecryptfs1:amd64				install
libedata-book-1.2-27t64:amd64			install
libedata-cal-2.0-2t64:amd64			install
libedataserver-1.2-27t64:amd64			install
libedataserverui-1.2-4t64:amd64			install
libedataserverui4-1.0-0t64:amd64		install
libedit2:amd64					install
libeditorconfig0:amd64				install
libefiboot1t64:amd64				install
libefivar1t64:amd64				install
libegl-mesa0:amd64				install
libegl1:amd64					install
libei1:amd64					install
libeis1:amd64					install
libel-api-java					install
libelf1t64:amd64				install
libemail-date-format-perl			install
libemf1:amd64					install
libenchant-2-2:amd64				install
libencode-eucjpascii-perl			install
libencode-eucjpms-perl				install
libencode-hanextra-perl				install
libencode-jis2k-perl				install
libencode-locale-perl				install
libencode-perl:amd64				install
libeot0:amd64					install
libepoxy0:amd64					install
libepub0					install
libepubgen-0.1-1:amd64				install
liberror-perl					install
libespeak-ng1:amd64				install
libestr0:amd64					install
libetonyek-0.1-1:amd64				install
libeval-closure-perl				install
libevdev2:amd64					install
libevent-2.1-7t64:amd64				install
libexception-class-perl				install
libexempi8:amd64				install
libexif12:amd64					install
libexiv2-27:amd64				install
libexpat1:amd64					install
libexporter-tiny-perl				install
libext2fs2t64:amd64				install
libexttextcat-2.0-0:amd64			install
libexttextcat-data				install
libextutils-depends-perl			install
libfaad2:amd64					install
libfakeroot:amd64				install
libfastjson4:amd64				install
libfbclient2:amd64				install
libfcgi-perl					install
libfcgi0t64:amd64				install
libfdisk1:amd64					install
libffi8:amd64					install
libffmpegthumbnailer4v5:amd64			install
libfftw3-double3:amd64				install
libfftw3-single3:amd64				install
libfido2-1:amd64				install
libfile-basedir-perl				install
libfile-desktopentry-perl			install
libfile-fcntllock-perl				install
libfile-find-rule-perl				install
libfile-fnmatch-perl				install
libfile-homedir-perl				install
libfile-listing-perl				install
libfile-mimeinfo-perl				install
libfile-sharedir-perl				install
libfile-slurper-perl				install
libfile-which-perl				install
libflac++10:amd64				install
libflac12t64:amd64				install
libflashrom1:amd64				install
libflatpak0:amd64				install
libflite1:amd64					install
libfluidsynth3:amd64				install
libfmt9:amd64					install
libfont-afm-perl				install
libfontbox-java					install
libfontconfig1:amd64				install
libfontenc1:amd64				install
libfprint-2-2					install
libfprint-2-tod1:amd64				install
libfreeaptx0:amd64				install
libfreehand-0.1-1				install
libfreerdp-server3-3:amd64			install
libfreerdp3-3:amd64				install
libfreetype6:amd64				install
libfribidi0:amd64				install
libftdi1-2:amd64				install
libfuse2t64:amd64				install
libfuse3-3:amd64				install
libfwupd2:amd64					install
libgail-3-0t64:amd64				install
libgail-common:amd64				install
libgail18t64:amd64				install
libgamemode0:amd64				install
libgamemodeauto0:amd64				install
libgbm1:amd64					install
libgc1:amd64					install
libgcc-13-dev:amd64				install
libgcc-s1:amd64					install
libgcc-s1:i386					install
libgck-1-0:amd64				install
libgck-2-2:amd64				install
libgcr-4-4:amd64				install
libgcr-base-3-1:amd64				install
libgcr-ui-3-1:amd64				install
libgcrypt20:amd64				install
libgd3:amd64					install
libgdata-common					install
libgdata22:amd64				install
libgdbm-compat4t64:amd64			install
libgdbm6t64:amd64				install
libgdk-pixbuf-2.0-0:amd64			install
libgdk-pixbuf2.0-bin				install
libgdk-pixbuf2.0-common				install
libgdm1						install
libgedit-amtk-5-0:amd64				install
libgedit-amtk-5-common				install
libgedit-gtksourceview-300-0:amd64		install
libgedit-gtksourceview-300-common		install
libgee-0.8-2:amd64				install
libgeoclue-2-0:amd64				install
libgeocode-glib-2-0:amd64			install
libgexiv2-2:amd64				install
libgfortran5:amd64				install
libgif7:amd64					install
libgirepository-1.0-1:amd64			install
libgjs0g:amd64					install
libgl1:amd64					install
libgl1-mesa-dri:amd64				install
libgl1-mesa-dri:i386				deinstall
libglapi-mesa:amd64				install
libgles2:amd64					install
libglew2.2:amd64				install
libglib-object-introspection-perl		install
libglib-perl:amd64				install
libglib2.0-0t64:amd64				install
libglib2.0-bin					install
libglib2.0-data					install
libglibmm-2.4-1t64:amd64			install
libglibmm-2.68-1t64:amd64			install
libglu1-mesa:amd64				install
libglut3.12:amd64				install
libglvnd0:amd64					install
libglx-mesa0:amd64				install
libglx0:amd64					install
libgme0:amd64					install
libgmp10:amd64					install
libgnome-autoar-0-0:amd64			install
libgnome-bg-4-2t64:amd64			install
libgnome-bluetooth-3.0-13:amd64			install
libgnome-bluetooth-ui-3.0-13:amd64		install
libgnome-desktop-3-20t64:amd64			install
libgnome-desktop-4-2t64:amd64			install
libgnome-rr-4-2t64:amd64			install
libgnomekbd-common				install
libgnomekbd8:amd64				install
libgnutls30t64:amd64				install
libgoa-1.0-0b:amd64				install
libgoa-1.0-common				install
libgoa-backend-1.0-2:amd64			install
libgomp1:amd64					install
libgpg-error0:amd64				install
libgpgme11t64:amd64				install
libgpgmepp6t64:amd64				install
libgphoto2-6t64:amd64				install
libgphoto2-l10n					install
libgphoto2-port12t64:amd64			install
libgpm2:amd64					install
libgpod-common					install
libgpod4t64:amd64				install
libgprofng0:amd64				install
libgraphene-1.0-0:amd64				install
libgraphicsmagick++-q16-12t64			install
libgraphicsmagick-q16-3t64			install
libgraphite2-3:amd64				install
libgrilo-0.3-0:amd64				install
libgs-common					install
libgs10:amd64					install
libgs10-common					install
libgsasl18:amd64				install
libgsf-1-114:amd64				install
libgsf-1-common					install
libgsf-bin					install
libgsl27:amd64					install
libgslcblas0:amd64				install
libgsm1:amd64					install
libgsound0t64:amd64				install
libgspell-1-2:amd64				install
libgspell-1-common				install
libgssapi-krb5-2:amd64				install
libgssdp-1.6-0:amd64				install
libgssglue1:amd64				install
libgstreamer-gl1.0-0:amd64			install
libgstreamer-plugins-bad1.0-0:amd64		install
libgstreamer-plugins-base1.0-0:amd64		install
libgstreamer-plugins-good1.0-0:amd64		install
libgstreamer1.0-0:amd64				install
libgtk-3-0t64:amd64				install
libgtk-3-bin					install
libgtk-3-common					install
libgtk-4-1:amd64				install
libgtk-4-common					install
libgtk-4-media-gstreamer			install
libgtk-layer-shell0				install
libgtk2.0-0t64:amd64				install
libgtk2.0-bin					install
libgtk2.0-common				install
libgtk3-perl					install
libgtkmm-3.0-1t64:amd64				install
libgtkmm-4.0-0:amd64				install
libgtksourceview-3.0-1:amd64			install
libgtksourceview-3.0-common			install
libgtksourceview-4-0:amd64			install
libgtksourceview-4-common			install
libgtksourceviewmm-3.0-0v5:amd64		install
libgtop-2.0-11:amd64				install
libgtop2-common					install
libgucharmap-2-90-7:amd64			install
libgudev-1.0-0:amd64				install
libgumbo2:amd64					install
libgupnp-1.6-0:amd64				install
libgupnp-av-1.0-3:amd64				install
libgupnp-dlna-2.0-4:amd64			install
libgupnp-igd-1.6-0:amd64			install
libgusb2:amd64					install
libgutenprint-common				install
libgutenprint9					install
libgweather-4-0t64:amd64			install
libgweather-4-common				install
libgxps2t64:amd64				install
libhandy-1-0:amd64				install
libharfbuzz-gobject0:amd64			install
libharfbuzz-icu0:amd64				install
libharfbuzz-subset0:amd64			install
libharfbuzz0b:amd64				install
libheif-plugin-aomdec:amd64			install
libheif-plugin-libde265:amd64			install
libheif1:amd64					install
libhfstospell11:amd64				install
libhogweed6t64:amd64				install
libhpmud0:amd64					install
libhsqldb1.8.0-java				install
libhtml-form-perl				install
libhtml-format-perl				install
libhtml-parser-perl:amd64			install
libhtml-tagset-perl				install
libhtml-tree-perl				install
libhttp-cookies-perl				install
libhttp-daemon-perl				install
libhttp-date-perl				install
libhttp-message-perl				install
libhttp-negotiate-perl				install
libhunspell-1.7-0:amd64				install
libhwasan0:amd64				install
libhwy1t64:amd64				install
libhyphen0:amd64				install
libib-util:amd64				install
libibus-1.0-5:amd64				install
libibverbs1:amd64				install
libical3t64:amd64				install
libice6:amd64					install
libicu74:amd64					install
libid3tag0:amd64				install
libidn12:amd64					install
libidn2-0:amd64					install
libidn2-0:i386					install
libiec61883-0:amd64				install
libieee1284-3t64:amd64				install
libigdgmm12:amd64				install
libijs-0.35:amd64				install
libimagequant0:amd64				install
libimath-3-1-29t64:amd64			install
libimobiledevice-utils				install
libimobiledevice6:amd64				install
libinih1:amd64					install
libinput-bin					install
libinput10:amd64				install
libinstpatch-1.0-2:amd64			install
libintl-perl					install
libintl-xs-perl					install
libio-html-perl					install
libio-socket-ssl-perl				install
libio-string-perl				install
libio-stringy-perl				install
libip4tc2:amd64					install
libip6tc2:amd64					install
libipc-run3-perl				install
libipc-shareable-perl				install
libipc-system-simple-perl			install
libipt2						install
libisl23:amd64					install
libisofs6t64:amd64				install
libitm1:amd64					install
libiw30t64:amd64				install
libixml11t64:amd64				install
libjack-jackd2-0:amd64				install
libjansson4:amd64				install
libjavascriptcoregtk-4.1-0:amd64		install
libjavascriptcoregtk-6.0-1:amd64		install
libjbig0:amd64					install
libjbig2dec0:amd64				install
libjcat1:amd64					install
libjcode-pm-perl				install
libjpeg-turbo-progs				install
libjpeg-turbo8:amd64				install
libjpeg8:amd64					install
libjs-excanvas					install
libjs-jquery					install
libjs-jquery-flot				install
libjs-jquery-ui					install
libjs-mathjax					install
libjs-sphinxdoc					install
libjs-underscore				install
libjson-c5:amd64				install
libjson-glib-1.0-0:amd64			install
libjson-glib-1.0-common				install
libjson-perl					install
libjson-xs-perl					install
libjsp-api-java					install
libjxl-tools					install
libjxl0.7:amd64					install
libjxr-tools					install
libjxr0t64:amd64				install
libk5crypto3:amd64				install
libkaccounts2:amd64				install
libkate1:amd64					install
libkeybinder-3.0-0:amd64			install
libkeyutils1:amd64				install
libkf5activities5:amd64				install
libkf5archive-data				install
libkf5archive5:amd64				install
libkf5attica5:amd64				install
libkf5auth-data					install
libkf5authcore5:amd64				install
libkf5bluezqt-data				install
libkf5bluezqt6:amd64				install
libkf5bookmarks-data				install
libkf5bookmarks5:amd64				install
libkf5calendarevents5:amd64			install
libkf5codecs-data				install
libkf5codecs5:amd64				install
libkf5completion-data				install
libkf5completion5:amd64				install
libkf5config-bin				install
libkf5config-data				install
libkf5configcore5:amd64				install
libkf5configgui5:amd64				install
libkf5configwidgets-data			install
libkf5configwidgets5:amd64			install
libkf5coreaddons-data				install
libkf5coreaddons5:amd64				install
libkf5crash5:amd64				install
libkf5dbusaddons-bin				install
libkf5dbusaddons-data				install
libkf5dbusaddons5:amd64				install
libkf5declarative-data				install
libkf5declarative5:amd64			install
libkf5doctools5:amd64				install
libkf5globalaccel-bin				install
libkf5globalaccel-data				install
libkf5globalaccel5:amd64			install
libkf5globalaccelprivate5:amd64			install
libkf5guiaddons-bin				install
libkf5guiaddons-data				install
libkf5guiaddons5:amd64				install
libkf5i18n-data					install
libkf5i18n5:amd64				install
libkf5iconthemes-bin				install
libkf5iconthemes-data				install
libkf5iconthemes5:amd64				install
libkf5itemviews-data				install
libkf5itemviews5:amd64				install
libkf5jobwidgets-data				install
libkf5jobwidgets5:amd64				install
libkf5js5t64:amd64				install
libkf5kexiv2-15.0.0:amd64			install
libkf5khtml-bin					install
libkf5khtml-data				install
libkf5khtml5:amd64				install
libkf5kiocore5:amd64				install
libkf5kiofilewidgets5:amd64			install
libkf5kiogui5:amd64				install
libkf5kiontlm5:amd64				install
libkf5kiowidgets5:amd64				install
libkf5kirigami2-5				install
libkf5newstuff-data				install
libkf5newstuff5:amd64				install
libkf5newstuffcore5:amd64			install
libkf5newstuffwidgets5:amd64			install
libkf5notifications-data			install
libkf5notifications5:amd64			install
libkf5package-data				install
libkf5package5:amd64				install
libkf5parts-data				install
libkf5parts-plugins:amd64			install
libkf5parts5:amd64				install
libkf5plasma5:amd64				install
libkf5plasmaquick5:amd64			install
libkf5prison5:amd64				install
libkf5pty-data					install
libkf5pty5:amd64				install
libkf5purpose-bin:amd64				install
libkf5purpose5:amd64				install
libkf5quickaddons5:amd64			install
libkf5service-bin				install
libkf5service-data				install
libkf5service5:amd64				install
libkf5solid5:amd64				install
libkf5solid5-data				install
libkf5sonnet5-data				install
libkf5sonnetcore5:amd64				install
libkf5sonnetui5:amd64				install
libkf5syndication5abi1:amd64			install
libkf5syntaxhighlighting-data			install
libkf5syntaxhighlighting5:amd64			install
libkf5texteditor-bin				install
libkf5texteditor5:amd64				install
libkf5textwidgets-data				install
libkf5textwidgets5:amd64			install
libkf5threadweaver5:amd64			install
libkf5wallet-bin				install
libkf5wallet-data				install
libkf5wallet5:amd64				install
libkf5waylandclient5:amd64			install
libkf5widgetsaddons-data			install
libkf5widgetsaddons5:amd64			install
libkf5windowsystem-data				install
libkf5windowsystem5:amd64			install
libkf5xmlgui-bin:amd64				install
libkf5xmlgui-data				install
libkf5xmlgui5:amd64				install
libklibc:amd64					install
libkmod2:amd64					install
libkpathsea6:amd64				install
libkrb5-3:amd64					install
libkrb5support0:amd64				install
libksba8:amd64					install
libkwalletbackend5-5:amd64			install
liblangtag-common				install
liblangtag1:amd64				install
liblapack3:amd64				install
liblatex-tounicode-perl				install
liblbfgsb0:amd64				install
liblc3-1:amd64					install
liblcms2-2:amd64				install
liblcms2-utils					install
libldacbt-abr2:amd64				install
libldacbt-enc2:amd64				install
libldap2:amd64					install
libldb2:amd64					install
liblerc4:amd64					install
liblibreoffice-java				install
liblightdm-gobject-1-0:amd64			install
liblilv-0-0:amd64				install
liblingua-translit-perl				install
liblirc-client0t64:amd64			install
liblist-allutils-perl				install
liblist-moreutils-perl				install
liblist-moreutils-xs-perl			install
liblist-someutils-perl				install
liblist-someutils-xs-perl:amd64			install
liblist-utilsby-perl				install
libllvm18:amd64					install
libllvm19:amd64					install
libllvm20:amd64					install
liblmdb0:amd64					install
liblocale-gettext-perl				install
liblockfile-bin					install
liblockfile1:amd64				install
liblog-dispatch-perl				install
liblog-log4perl-perl				install
liblouis-data					install
liblouis20:amd64				install
liblouisutdml-bin				install
liblouisutdml-data				install
liblouisutdml9t64:amd64				install
liblqr-1-0:amd64				install
liblrdf0:amd64					install
liblsan0:amd64					install
libltc11:amd64					install
libltdl7:amd64					install
liblua5.2-0:amd64				install
liblua5.4-0:amd64				install
liblvm2cmd2.03:amd64				install
liblwp-mediatypes-perl				install
liblwp-protocol-https-perl			install
liblz4-1:amd64					install
liblzma5:amd64					install
liblzma5:i386					install
liblzo2-2:amd64					install
libmad0:amd64					install
libmagic-mgc					install
libmagic1t64:amd64				install
libmagickcore-6.q16-7-extra:amd64		install
libmagickcore-6.q16-7t64:amd64			install
libmagickwand-6.q16-7t64:amd64			install
libmail-sendmail-perl				install
libmailtools-perl				install
libmailutils9t64:amd64				install
libmalcontent-0-0:amd64				install
libmanette-0.2-0:amd64				install
libmarkdown2:amd64				install
libmate-desktop-2-17t64:amd64			install
libmate-menu2:amd64				install
libmate-panel-applet-4-1:amd64			install
libmateweather-common				install
libmateweather1t64:amd64			install
libmatroska7:amd64				install
libmaxminddb0:amd64				install
libmbedcrypto7t64:amd64				install
libmbim-glib4:amd64				install
libmbim-proxy					install
libmd0:amd64					install
libmd0:i386					install
libmd4c0:amd64					install
libmediaart-2.0-0:amd64				install
libmetacity3:amd64				install
libmfx1:amd64					install
libmhash2:amd64					install
libmime-charset-perl				install
libmime-lite-perl				install
libmime-types-perl				install
libminiupnpc17:amd64				install
libminizip1t64:amd64				install
libmjpegutils-2.1-0t64:amd64			install
libmm-glib0:amd64				install
libmng2:amd64					install
libmnl0:amd64					install
libmodplug1:amd64				install
libmodule-find-perl				install
libmodule-implementation-perl			install
libmodule-runtime-perl				install
libmodule-scandeps-perl				install
libmount1:amd64					install
libmozjs-115-0t64:amd64				install
libmp3lame0:amd64				install
libmpc3:amd64					install
libmpcdec6:amd64				install
libmpeg2-4:amd64				install
libmpeg2encpp-2.1-0t64:amd64			install
libmpfr6:amd64					install
libmpg123-0t64:amd64				install
libmplex2-2.1-0t64:amd64			install
libmpv2:amd64					install
libmro-compat-perl				install
libmsgraph-0-1:amd64				install
libmspack0t64:amd64				install
libmspub-0.1-1:amd64				install
libmtdev1t64:amd64				install
libmtp-common					install
libmtp-runtime					install
libmtp9t64:amd64				install
libmuffin0:amd64				install
libmujs3:amd64					install
libmusicbrainz5-2:amd64				install
libmusicbrainz5cc2v5:amd64			install
libmutter-14-0:amd64				install
libmwaw-0.3-3:amd64				install
libmysofa1:amd64				install
libmysqlclient21:amd64				install
libmythes-1.2-0:amd64				install
libnamespace-autoclean-perl			install
libnamespace-clean-perl				install
libnatpmp1t64:amd64				install
libnautilus-extension4:amd64			install
libncurses6:amd64				install
libncursesw6:amd64				install
libndp0:amd64					install
libnemo-extension1:amd64			install
libneon27t64:amd64				install
libneon27t64-gnutls:amd64			install
libnet-dbus-perl				install
libnet-http-perl				install
libnet-libidn-perl				install
libnet-smtp-ssl-perl				install
libnet-ssleay-perl:amd64			install
libnetfilter-conntrack3:amd64			install
libnetpbm11t64:amd64				install
libnetplan1:amd64				install
libnettle8t64:amd64				install
libnewt0.52:amd64				install
libnfnetlink0:amd64				install
libnfs14:amd64					install
libnftables1:amd64				install
libnftnl11:amd64				install
libnghttp2-14:amd64				install
libnghttp3-3:amd64				install
libnice10:amd64					install
libnl-3-200:amd64				install
libnl-genl-3-200:amd64				install
libnl-route-3-200:amd64				install
libnm0:amd64					install
libnma-common					install
libnma-gtk4-0:amd64				install
libnma0:amd64					install
libnorm1t64:amd64				install
libnotify-bin					install
libnotify4:amd64				install
libnpth0t64:amd64				install
libnsl2:amd64					install
libnspr4:amd64					install
libnss-mdns:amd64				install
libnss-myhostname:amd64				install
libnss-systemd:amd64				install
libnss3:amd64					install
libntfs-3g89t64:amd64				install
libntlm0:amd64					install
libnuma1:amd64					install
libnumber-compare-perl				install
libnvidia-compute-535:amd64			install
libnvme1t64					install
libodfgen-0.1-1:amd64				install
libogg0:amd64					install
libokular5core11				install
libole-storage-lite-perl			install
libopenal-data					install
libopenal1:amd64				install
libopencore-amrnb0:amd64			install
libopencore-amrwb0:amd64			install
libopenexr-3-1-30:amd64				install
libopengl0:amd64				install
libopenh264-7:amd64				install
libopenjp2-7:amd64				install
libopenmpt-modplug1:amd64			install
libopenmpt0t64:amd64				install
libopenni2-0:amd64				install
libopus0:amd64					install
libopusfile0:amd64				install
liborc-0.4-0t64:amd64				install
liborcus-0.18-0:amd64				install
liborcus-parser-0.18-0:amd64			install
libosp5						install
libostree-1-1:amd64				install
libostyle1t64					install
libp11-kit0:amd64				install
libpackage-stash-perl				install
libpackage-stash-xs-perl:amd64			install
libpackagekit-glib2-18:amd64			install
libpadwalker-perl				install
libpagemaker-0.0-0:amd64			install
libpam-cap:amd64				install
libpam-fingwit					install
libpam-fprintd:amd64				install
libpam-gnome-keyring:amd64			install
libpam-modules:amd64				install
libpam-modules-bin				install
libpam-runtime					install
libpam-systemd:amd64				install
libpam-tmpdir					install
libpam0g:amd64					install
libpango-1.0-0:amd64				install
libpangocairo-1.0-0:amd64			install
libpangoft2-1.0-0:amd64				install
libpangomm-1.4-1v5:amd64			install
libpangomm-2.48-1t64:amd64			install
libpangoxft-1.0-0:amd64				install
libpaper-utils					install
libpaper1:amd64					install
libparams-classify-perl:amd64			install
libparams-util-perl				install
libparams-validate-perl:amd64			install
libparams-validationcompiler-perl		install
libparse-recdescent-perl			install
libparted2t64:amd64				install
libpcap0.8t64:amd64				install
libpcaudio0:amd64				install
libpci3:amd64					install
libpciaccess0:amd64				install
libpcre2-16-0:amd64				install
libpcre2-32-0:amd64				install
libpcre2-8-0:amd64				install
libpcre2-posix3:amd64				install
libpcre3:amd64					install
libpcsclite1:amd64				install
libpdfbox-java					install
libpeas-1.0-0:amd64				install
libpeas-common					install
libperl5.38t64:amd64				install
libperlio-gzip-perl				install
libperlio-utf8-strict-perl			install
libpgm-5.3-0t64:amd64				install
libphonenumber8:amd64				install
libphonon-l10n					install
libphonon4qt5-4t64:amd64			install
libpipeline1:amd64				install
libpipewire-0.3-0t64:amd64			install
libpipewire-0.3-modules:amd64			install
libpixman-1-0:amd64				install
libpkcs11-helper1t64:amd64			install
libpkgconf3:amd64				install
libplacebo338:amd64				install
libplist-2.0-4:amd64				install
libplot2c2:amd64				install
libplymouth5:amd64				install
libpng16-16t64:amd64				install
libpocketsphinx3:amd64				install
libpodofo0.9.8t64				install
libpolkit-agent-1-0:amd64			install
libpolkit-gobject-1-0:amd64			install
libpolkit-qt5-1-1:amd64				install
libpoppler-cpp0t64:amd64			install
libpoppler-glib8t64:amd64			install
libpoppler-qt5-1t64:amd64			install
libpoppler-qt6-3t64:amd64			install
libpoppler134:amd64				install
libpopt0:amd64					install
libportaudio2:amd64				install
libportmidi0:amd64				install
libportsmf0t64:amd64				install
libpostproc57:amd64				install
libpotrace0:amd64				install
libppd2:amd64					install
libppd2-common					install
libpq5:amd64					install
libproc-processtable-perl:amd64			install
libproc2-0:amd64				install
libprotobuf-c1:amd64				install
libprotobuf-lite32t64:amd64			install
libprotobuf32t64:amd64				install
libproxy-tools					install
libproxy1-plugin-gsettings:amd64		install
libproxy1-plugin-networkmanager:amd64		install
libproxy1v5:amd64				install
libpsl5t64:amd64				install
libpstoedit0t64:amd64				install
libptexenc1:amd64				install
libpugixml1v5:amd64				install
libpulse-mainloop-glib0:amd64			install
libpulse0:amd64					install
libpwquality-common				install
libpwquality1:amd64				install
libpython3-stdlib:amd64				install
libpython3.12-minimal:amd64			install
libpython3.12-stdlib:amd64			install
libpython3.12t64:amd64				install
libqb100:amd64					install
libqca-qt5-2:amd64				install
libqca-qt5-2-plugins:amd64			install
libqhull-r8.0:amd64				install
libqmi-glib5:amd64				install
libqmi-proxy					install
libqmobipocket2:amd64				install
libqpdf29t64:amd64				install
libqrencode4:amd64				install
libqrtr-glib0:amd64				install
libqt5core5t64:amd64				install
libqt5dbus5t64:amd64				install
libqt5designer5:amd64				install
libqt5gui5t64:amd64				install
libqt5help5:amd64				install
libqt5multimedia5:amd64				install
libqt5network5t64:amd64				install
libqt5networkauth5:amd64			install
libqt5positioning5:amd64			install
libqt5printsupport5t64:amd64			install
libqt5qml5:amd64				install
libqt5qmlmodels5:amd64				install
libqt5qmlworkerscript5:amd64			install
libqt5quick5:amd64				install
libqt5quickcontrols2-5:amd64			install
libqt5quicktemplates2-5:amd64			install
libqt5quickwidgets5:amd64			install
libqt5script5:amd64				install
libqt5sql5-sqlite:amd64				install
libqt5sql5t64:amd64				install
libqt5svg5:amd64				install
libqt5test5t64:amd64				install
libqt5texttospeech5:amd64			install
libqt5waylandclient5:amd64			install
libqt5waylandcompositor5:amd64			install
libqt5webchannel5:amd64				install
libqt5webengine-data				install
libqt5webengine5:amd64				install
libqt5webenginecore5:amd64			install
libqt5webenginewidgets5:amd64			install
libqt5widgets5t64:amd64				install
libqt5x11extras5:amd64				install
libqt5xml5t64:amd64				install
libqt5xmlpatterns5:amd64			install
libqt6concurrent6t64:amd64			install
libqt6core5compat6:amd64			install
libqt6core6t64:amd64				install
libqt6dbus6t64:amd64				install
libqt6gui6t64:amd64				install
libqt6multimedia6:amd64				install
libqt6network6t64:amd64				install
libqt6opengl6t64:amd64				install
libqt6openglwidgets6t64:amd64			install
libqt6positioning6:amd64			install
libqt6printsupport6t64:amd64			install
libqt6qml6:amd64				install
libqt6qmlmodels6:amd64				install
libqt6quick6:amd64				install
libqt6quickwidgets6:amd64			install
libqt6sql6-sqlite:amd64				install
libqt6sql6t64:amd64				install
libqt6svg6:amd64				install
libqt6svgwidgets6:amd64				install
libqt6test6t64:amd64				install
libqt6uitools6:amd64				install
libqt6waylandclient6:amd64			install
libqt6waylandcompositor6:amd64			install
libqt6waylandeglclienthwintegration6:amd64	install
libqt6waylandeglcompositorhwintegration6:amd64	install
libqt6webchannel6:amd64				install
libqt6webengine6-data				install
libqt6webenginecore6:amd64			install
libqt6webenginecore6-bin			install
libqt6webenginequick6:amd64			install
libqt6webenginewidgets6:amd64			install
libqt6widgets6t64:amd64				install
libqt6wlshellintegration6:amd64			install
libqt6xml6t64:amd64				install
libquadmath0:amd64				install
libquazip1-qt6-1t64:amd64			install
librabbitmq4:amd64				install
libraptor2-0:amd64				install
libraqm0:amd64					install
librasqal3t64:amd64				install
librav1e0:amd64					install
libraw1394-11:amd64				install
libraw23t64:amd64				install
librda-common					install
librda0:amd64					install
librdf0t64:amd64				install
libre2-10:amd64					install
libreadline8t64:amd64				install
libreadonly-perl				install
libref-util-perl				install
libref-util-xs-perl				install
libregexp-common-perl				install
libreiserfscore0t64				install
libreoffice					install
libreoffice-base				install
libreoffice-base-core				install
libreoffice-base-drivers			install
libreoffice-calc				install
libreoffice-common				install
libreoffice-core				install
libreoffice-draw				install
libreoffice-gnome				install
libreoffice-gtk3				install
libreoffice-help-common				install
libreoffice-help-en-us				install
libreoffice-help-nl				install
libreoffice-impress				install
libreoffice-java-common				install
libreoffice-l10n-nl				install
libreoffice-math				install
libreoffice-nlpsolver				install
libreoffice-report-builder			install
libreoffice-report-builder-bin			install
libreoffice-script-provider-bsh			install
libreoffice-script-provider-js			install
libreoffice-script-provider-python		install
libreoffice-sdbc-firebird			install
libreoffice-sdbc-hsqldb				install
libreoffice-sdbc-mysql				install
libreoffice-sdbc-postgresql			install
libreoffice-style-colibre			install
libreoffice-uiconfig-base			install
libreoffice-uiconfig-calc			install
libreoffice-uiconfig-common			install
libreoffice-uiconfig-draw			install
libreoffice-uiconfig-impress			install
libreoffice-uiconfig-math			install
libreoffice-uiconfig-report-builder		install
libreoffice-uiconfig-writer			install
libreoffice-wiki-publisher			install
libreoffice-writer				install
libresid-builder0c2a				install
librest-1.0-0:amd64				install
librevenge-0.0-0:amd64				install
librhythmbox-core10:amd64			install
librist4:amd64					install
libroc0.3:amd64					install
librole-tiny-perl				install
librsvg2-2:amd64				install
librsvg2-common:amd64				install
librtmp1:amd64					install
librubberband2:amd64				install
libruby:amd64					install
libruby3.2:amd64				install
librygel-core-2.8-0:amd64			install
librygel-db-2.8-0:amd64				install
librygel-renderer-2.8-0:amd64			install
librygel-server-2.8-0:amd64			install
libsamplerate0:amd64				install
libsane-common					install
libsane-hpaio:amd64				install
libsane1:amd64					install
libsasl2-2:amd64				install
libsasl2-modules:amd64				install
libsasl2-modules-db:amd64			install
libsasl2-modules-gssapi-mit:amd64		install
libsbc1:amd64					install
libsbsms10:amd64				install
libsdl2-2.0-0:amd64				install
libseccomp2:amd64				install
libsecret-1-0:amd64				install
libsecret-common				install
libselinux1:amd64				install
libsemanage-common				install
libsemanage2:amd64				install
libsensors-config				install
libsensors5:amd64				install
libsepol2:amd64					install
libserd-0-0:amd64				install
libservlet-api-java				install
libservlet3.1-java				install
libsframe1:amd64				install
libsgutils2-1.46-2:amd64			install
libsharpyuv0:amd64				install
libshine3:amd64					install
libshout3:amd64					install
libsidplay1v5:amd64				install
libsidplay2					install
libsigc++-2.0-0v5:amd64				install
libsigc++-3.0-0:amd64				install
libsignon-plugins-common1:amd64			install
libsignon-qt5-1:amd64				install
libsigsegv2:amd64				install
libsixel1:amd64					install
libslang2:amd64					install
libsm6:amd64					install
libsmartcols1:amd64				install
libsmbclient0:amd64				install
libsmi2t64:amd64				install
libsnapd-glib-2-1:amd64				install
libsnappy1v5:amd64				install
libsndfile1:amd64				install
libsndio7.0:amd64				install
libsnmp-base					install
libsnmp40t64:amd64				install
libsocket6-perl					install
libsodium23:amd64				install
libsombok3:amd64				install
libsonic0:amd64					install
libsord-0-0:amd64				install
libsort-key-perl				install
libsort-naturally-perl				install
libsoundtouch1:amd64				install
libsoup-2.4-1:amd64				install
libsoup-3.0-0:amd64				install
libsoup-3.0-common				install
libsoup-gnome-2.4-1:amd64			install
libsoup2.4-common				install
libsource-highlight-common			install
libsource-highlight4t64:amd64			install
libsoxr0:amd64					install
libspa-0.2-bluetooth:amd64			install
libspa-0.2-modules:amd64			install
libspandsp2t64:amd64				install
libspatialaudio0t64:amd64			install
libspecio-perl					install
libspectre1:amd64				install
libspeechd2:amd64				install
libspeex1:amd64					install
libspeexdsp1:amd64				install
libsphinxbase3t64:amd64				install
libspreadsheet-parseexcel-perl			install
libspreadsheet-writeexcel-perl			install
libsqlite3-0:amd64				install
libsratom-0-0:amd64				install
libsrt1.5-gnutls:amd64				install
libsrtp2-1:amd64				install
libss2:amd64					install
libssh-4:amd64					install
libssh-gcrypt-4:amd64				install
libssh2-1t64:amd64				install
libssl3t64:amd64				install
libstartup-notification0:amd64			install
libstdc++-13-dev:amd64				install
libstdc++6:amd64				install
libstemmer0d:amd64				install
libstring-crc32-perl				install
libsub-exporter-perl				install
libsub-exporter-progressive-perl		install
libsub-identify-perl				install
libsub-install-perl				install
libsub-name-perl:amd64				install
libsub-quote-perl				install
libsuil-0-0:amd64				install
libsuitesparseconfig7:amd64			install
libsvtav1enc1d1:amd64				install
libswresample4:amd64				install
libswscale7:amd64				install
libsynctex2:amd64				install
libsys-hostname-long-perl			install
libsystemd-shared:amd64				install
libsystemd0:amd64				install
libtag1v5:amd64					install
libtag1v5-vanilla:amd64				install
libtalloc2:amd64				install
libtasn1-6:amd64				install
libtcl8.6:amd64					install
libtcmalloc-minimal4t64:amd64			install
libtdb1:amd64					install
libteamdctl0:amd64				install
libteckit0:amd64				install
libtepl-6-4:amd64				install
libtepl-common					install
libterm-readkey-perl				install
libtevent0t64:amd64				install
libtexlua53-5:amd64				install
libtext-bibtex-perl				install
libtext-charwidth-perl:amd64			install
libtext-csv-perl				install
libtext-csv-xs-perl:amd64			install
libtext-glob-perl				install
libtext-iconv-perl:amd64			install
libtext-roman-perl				install
libtext-unidecode-perl				install
libtext-wrapi18n-perl				install
libthai-data					install
libthai0:amd64					install
libtheora0:amd64				install
libtie-cycle-perl				install
libtie-ixhash-perl				install
libtiff6:amd64					install
libtimedate-perl				install
libtimezonemap-data				install
libtimezonemap1:amd64				install
libtinfo6:amd64					install
libtinfo6:i386					install
libtirpc-common					install
libtirpc3t64:amd64				install
libtk8.6:amd64					install
libtommath1:amd64				install
libtotem-plparser-common			install
libtotem-plparser18:amd64			install
libtraceevent1:amd64				install
libtry-tiny-perl				install
libts0t64:amd64					install
libtsan2:amd64					install
libtspi1					install
libtss2-esys-3.0.2-0t64:amd64			install
libtss2-mu-4.0.1-0t64:amd64			install
libtss2-rc0t64:amd64				install
libtss2-sys1t64:amd64				install
libtss2-tcti-cmd0t64:amd64			install
libtss2-tcti-device0t64:amd64			install
libtss2-tcti-libtpms0t64:amd64			install
libtss2-tcti-mssim0t64:amd64			install
libtss2-tcti-spi-helper0t64:amd64		install
libtss2-tcti-swtpm0t64:amd64			install
libtss2-tctildr0t64:amd64			install
libtumbler-1-0t64:amd64				install
libturbojpeg:amd64				install
libtwolame0:amd64				install
libtypes-serialiser-perl			install
libubsan1:amd64					install
libuchardet0:amd64				install
libudev1:amd64					install
libudfread0:amd64				install
libudisks2-0:amd64				install
libumockdev0:amd64				install
libunibreak5:amd64				install
libunicode-linebreak-perl			install
libunicode-map-perl				install
libunistring5:amd64				install
libunistring5:i386				install
libuno-cppu3t64					install
libuno-cppuhelpergcc3-3t64			install
libuno-purpenvhelpergcc3-3t64			install
libuno-sal3t64					install
libuno-salhelpergcc3-3t64			install
libunoloader-java				install
libunshield0:amd64				install
libunwind8:amd64				install
libupnp17t64:amd64				install
libupower-glib3:amd64				install
liburcu8t64:amd64				install
liburi-perl					install
liburing2:amd64					install
libusb-1.0-0:amd64				install
libusbguard1					install
libusbmuxd6:amd64				install
libutempter0:amd64				install
libuuid1:amd64					install
libuv1t64:amd64					install
libv4l-0t64:amd64				install
libv4lconvert0t64:amd64				install
libva-drm2:amd64				install
libva-wayland2:amd64				install
libva-x11-2:amd64				install
libva2:amd64					install
libvamp-hostsdk3v5:amd64			install
libvariable-magic-perl				install
libvdpau1:amd64					install
libvidstab1.1:amd64				install
libvisio-0.1-1:amd64				install
libvisual-0.4-0:amd64				install
libvisual-0.4-plugins:amd64			install
libvlc-bin:amd64				install
libvlc5:amd64					install
libvlccore9:amd64				install
libvncclient1:amd64				install
libvo-aacenc0:amd64				install
libvo-amrwbenc0:amd64				install
libvoikko1:amd64				install
libvolume-key1:amd64				install
libvorbis0a:amd64				install
libvorbisenc2:amd64				install
libvorbisfile3:amd64				install
libvpl2						install
libvpx9:amd64					install
libvte-2.91-0:amd64				install
libvte-2.91-common				install
libvulkan1:amd64				install
libwacom-bin					install
libwacom-common					install
libwacom9:amd64					install
libwavpack1:amd64				install
libwayland-client0:amd64			install
libwayland-cursor0:amd64			install
libwayland-egl1:amd64				install
libwayland-server0:amd64			install
libwbclient0:amd64				install
libwebkit2gtk-4.1-0:amd64			install
libwebkitgtk-6.0-4:amd64			install
libwebp7:amd64					install
libwebpdemux2:amd64				install
libwebpmux3:amd64				install
libwebrtc-audio-processing1:amd64		install
libwebsocket-api-java				install
libwhoopsie-preferences0			install
libwhoopsie0:amd64				install
libwildmidi2:amd64				install
libwinpr3-3:amd64				install
libwireplumber-0.4-0:amd64			install
libwireshark-data				install
libwireshark17t64:amd64				install
libwiretap14t64:amd64				install
libwmf-0.2-7:amd64				install
libwmf-0.2-7-gtk:amd64				install
libwmf0.2-7-gtk:amd64				install
libwmflite-0.2-7:amd64				install
libwnck-3-0:amd64				install
libwnck-3-common				install
libwoff1:amd64					install
libwpd-0.10-10:amd64				install
libwpg-0.3-3:amd64				install
libwps-0.4-4:amd64				install
libwrap0:amd64					install
libwsutil15t64:amd64				install
libwww-perl					install
libwww-robotrules-perl				install
libwxbase3.2-1t64:amd64				install
libwxgtk3.2-1t64:amd64				install
libx11-6:amd64					install
libx11-data					install
libx11-protocol-perl				install
libx11-xcb1:amd64				install
libx264-164:amd64				install
libx265-199:amd64				install
libxapian30:amd64				install
libxapp1:amd64					install
libxatracker2:amd64				install
libxau6:amd64					install
libxaw7:amd64					install
libxcb-composite0:amd64				install
libxcb-damage0:amd64				install
libxcb-dri2-0:amd64				install
libxcb-dri3-0:amd64				install
libxcb-glx0:amd64				install
libxcb-icccm4:amd64				install
libxcb-image0:amd64				install
libxcb-keysyms1:amd64				install
libxcb-present0:amd64				install
libxcb-randr0:amd64				install
libxcb-record0:amd64				install
libxcb-render-util0:amd64			install
libxcb-render0:amd64				install
libxcb-res0:amd64				install
libxcb-shape0:amd64				install
libxcb-shm0:amd64				install
libxcb-sync1:amd64				install
libxcb-util1:amd64				install
libxcb-xfixes0:amd64				install
libxcb-xinerama0:amd64				install
libxcb-xinput0:amd64				install
libxcb-xkb1:amd64				install
libxcb-xv0:amd64				install
libxcb1:amd64					install
libxcomposite1:amd64				install
libxcursor1:amd64				install
libxcvt0:amd64					install
libxdamage1:amd64				install
libxdmcp6:amd64					install
libxdo3:amd64					install
libxext6:amd64					install
libxfce4ui-2-0:amd64				install
libxfce4ui-common				install
libxfce4util-bin				install
libxfce4util-common				install
libxfce4util7:amd64				install
libxfconf-0-3:amd64				install
libxfixes3:amd64				install
libxfont2:amd64					install
libxft2:amd64					install
libxi6:amd64					install
libxinerama1:amd64				install
libxkbcommon-x11-0:amd64			install
libxkbcommon0:amd64				install
libxkbfile1:amd64				install
libxkbregistry0:amd64				install
libxklavier16:amd64				install
libxml++2.6-2v5:amd64				install
libxml-libxml-perl				install
libxml-libxml-simple-perl			install
libxml-libxslt-perl:amd64			install
libxml-namespacesupport-perl			install
libxml-parser-perl				install
libxml-sax-base-perl				install
libxml-sax-expat-perl				install
libxml-sax-perl					install
libxml-twig-perl				install
libxml-writer-perl				install
libxml-xpathengine-perl				install
libxml2:amd64					install
libxmlb2:amd64					install
libxmlsec1t64:amd64				install
libxmlsec1t64-nss:amd64				install
libxmu6:amd64					install
libxmuu1:amd64					install
libxpm4:amd64					install
libxpresent1:amd64				install
libxrandr2:amd64				install
libxreaderdocument3				install
libxreaderview3					install
libxrender1:amd64				install
libxres1:amd64					install
libxshmfence1:amd64				install
libxslt1.1:amd64				install
libxss1:amd64					install
libxstring-perl:amd64				install
libxt6t64:amd64					install
libxtables12:amd64				install
libxtst6:amd64					install
libxv1:amd64					install
libxvidcore4:amd64				install
libxvmc1:amd64					install
libxxf86dga1:amd64				install
libxxf86vm1:amd64				install
libxxhash0:amd64				install
libyajl2:amd64					install
libyaml-0-2:amd64				install
libyaml-tiny-perl				install
libyara10:amd64					install
libyelp0:amd64					install
libzbar0t64:amd64				install
libzimg2:amd64					install
libzip4t64:amd64				install
libzix-0-0:amd64				install
libzmq5:amd64					install
libzstd1:amd64					install
libzstd1:i386					install
libzvbi-common					install
libzvbi0t64:amd64				install
libzxing3:amd64					install
libzzip-0-13t64:amd64				install
lightdm						install
lightdm-settings				install
linux-base					install
linux-firmware					install
linux-generic					install
linux-generic-hwe-24.04				install
linux-headers-6.14.0-37-generic			install
linux-headers-6.8.0-90				install
linux-headers-6.8.0-90-generic			install
linux-headers-generic				install
linux-headers-generic-hwe-24.04			install
linux-hwe-6.14-headers-6.14.0-29		install
linux-hwe-6.14-headers-6.14.0-37		install
linux-hwe-6.14-tools-6.14.0-36			install
linux-hwe-6.14-tools-6.14.0-37			install
linux-image-6.14.0-37-generic			install
linux-image-6.8.0-90-generic			install
linux-image-generic				install
linux-image-generic-hwe-24.04			install
linux-libc-dev:amd64				install
linux-modules-6.14.0-37-generic			install
linux-modules-6.8.0-90-generic			install
linux-modules-extra-6.14.0-37-generic		install
linux-modules-extra-6.8.0-90-generic		install
linux-sound-base				install
linux-tools-6.14.0-37-generic			install
linux-tools-6.8.0-90				install
linux-tools-6.8.0-90-generic			install
linux-tools-common				install
linuxmint-keyring				install
lm-sensors					install
lmodern						install
localechooser-data				install
locales						install
login						install
logrotate					install
logsave						install
lp-solve					install
lsb-release					install
lshw						install
lsof						install
lto-disabled-list				install
ltrace						install
luametatex					install
lvm2						install
lynis						install
lzip						install
lzop						install
m4						install
mailcap						install
mailutils					install
mailutils-common				install
make						install
man-db						install
manpages					install
mate-desktop					install
mate-desktop-common				install
mate-menus					install
mate-panel					install
mate-panel-common				install
mate-polkit					install
mate-polkit-common				install
mathomatic					install
mawk						install
mdadm						install
media-player-info				install
media-types					install
meld						install
menu						install
mesa-libgallium:amd64				install
mesa-utils					install
mesa-utils-bin:amd64				install
mesa-va-drivers:amd64				install
mesa-vdpau-drivers:amd64			install
mesa-vulkan-drivers:amd64			install
metacity					install
metacity-common					install
mint-artwork					install
mint-backgrounds-wallpapers			install
mint-common					install
mint-cursor-themes				install
mint-info-cinnamon				install
mint-l-icons					install
mint-l-theme					install
mint-meta-cinnamon				install
mint-meta-codecs				install
mint-meta-core					install
mint-mirrors					install
mint-themes					install
mint-translations				install
mint-upgrade-info				install
mint-x-icons					install
mint-y-icons					install
mintbackup					install
mintdrivers					install
mintinstall					install
mintreport					install
mintsources					install
mintstick					install
mintsysadm					install
mintsystem					install
mintupdate					install
mintwelcome					install
mobile-broadband-provider-info			install
modemmanager					install
mokutil						install
mount						install
mousetweaks					install
mscompress					install
mtools						install
mtr-tiny					install
muffin						install
muffin-common					install
muffin-dbg					install
mupdf-tools					install
mutter-common					install
mutter-common-bin				install
mysql-common					install
mythes-en-us					install
nano						install
nautilus-data					install
ncurses-base					install
ncurses-bin					install
needrestart					install
nemo						install
nemo-data					install
nemo-emblems					install
nemo-fileroller					install
nemo-share					install
neofetch					install
net-tools					install
netbase						install
netcat-openbsd					install
netpbm						install
netplan-generator				install
netplan.io					install
network-manager					install
network-manager-config-connectivity-ubuntu	install
network-manager-gnome				install
network-manager-openvpn				install
network-manager-openvpn-gnome			install
network-manager-pptp				install
network-manager-pptp-gnome			install
networkd-dispatcher				install
nftables					install
ntfs-3g						install
numlockx					install
ocl-icd-libopencl1:amd64			install
okular						install
okular-extra-backends				install
onboard						install
onboard-common					install
openjade					install
openjdk-21-jre:amd64				install
openjdk-21-jre-headless:amd64			install
openprinting-ppds				install
openssl						install
openvpn						install
optipng						install
orca						install
os-prober					install
p11-kit						install
p11-kit-modules:amd64				install
p7zip						install
p7zip-full					install
packagekit					install
packagekit-tools				install
papirus-icon-theme				install
parted						install
passwd						install
patch						install
patchutils					install
pavucontrol					install
pci.ids						install
pciutils					install
pcmciautils					install
pdfarranger					install
perl						install
perl-base					install
perl-modules-5.38				install
perl-openssl-defaults:amd64			install
pfb2t1c2pfb					install
phonon-backend-vlc-common			install
phonon4qt5:amd64				install
phonon4qt5-backend-vlc:amd64			install
pigz						install
pinentry-curses					install
pinentry-gnome3					install
pipewire:amd64					install
pipewire-alsa:amd64				install
pipewire-audio					install
pipewire-bin					install
pipewire-pulse					install
pix						install
pix-data					install
pkexec						install
pkg-config:amd64				install
pkgconf:amd64					install
pkgconf-bin					install
plasma-framework				install
plocate						install
plymouth					install
plymouth-label					install
plymouth-theme-spinner				install
plymouth-theme-ubuntu-text			install
pm-utils					install
policykit-1					install
policykit-1-gnome				install
policykit-desktop-privileges			install
polkitd						install
poppler-data					install
poppler-utils					install
postfix						install
power-profiles-daemon				install
powermgmt-base					install
ppp						install
pptp-linux					install
prerex						install
preview-latex-style				install
procps						install
ps2eps						install
psmisc						install
pstoedit					install
psutils						install
publicsuffix					install
pulseaudio-utils				install
purifyeps					install
pyqt6-dev-tools					install
python-apt-common				install
python-babel-localedata				install
python-matplotlib-data				install
python-nemo					install
python-tinycss2-common				install
python3						install
python3-apparmor				install
python3-appdirs					install
python3-apport					install
python3-apsw					install
python3-apt					install
python3-aptdaemon				install
python3-aptdaemon.gtk3widgets			install
python3-asttokens				install
python3-async-timeout				install
python3-attr					install
python3-babel					install
python3-blinker					install
python3-bpfcc					install
python3-brlapi:amd64				install
python3-brotli					install
python3-bs4					install
python3-cairo					install
python3-certifi					install
python3-cffi-backend:amd64			install
python3-chardet					install
python3-chm					install
python3-click					install
python3-colorama				install
python3-commandnotfound				install
python3-configobj				install
python3-contourpy				install
python3-cryptography				install
python3-css-parser				install
python3-cssselect				install
python3-cups:amd64				install
python3-cupshelpers				install
python3-cycler					install
python3-dateutil				install
python3-dbus					install
python3-debconf					install
python3-debian					install
python3-decorator				install
python3-defer					install
python3-deprecated				install
python3-deprecation				install
python3-dill					install
python3-distro					install
python3-dnspython				install
python3-executing				install
python3-eyed3					install
python3-feedparser				install
python3-filelock				install
python3-filetype				install
python3-fonttools				install
python3-fs					install
python3-gdbm:amd64				install
python3-gi					install
python3-gi-cairo				install
python3-gnupg					install
python3-html2text				install
python3-html5-parser				install
python3-html5lib				install
python3-httplib2				install
python3-ibus-1.0				install
python3-icu					install
python3-idna					install
python3-ifaddr					install
python3-imdbpy					install
python3-img2pdf					install
python3-ipython					install
python3-jedi					install
python3-jeepney					install
python3-json-pointer				install
python3-jsonschema				install
python3-jwt					install
python3-kiwisolver				install
python3-launchpadlib				install
python3-lazr.restfulclient			install
python3-lazr.uri				install
python3-ldb					install
python3-libapparmor				install
python3-libevdev				install
python3-louis					install
python3-lxml:amd64				install
python3-lz4					install
python3-mako					install
python3-markdown				install
python3-markdown-it				install
python3-markupsafe				install
python3-matplotlib				install
python3-matplotlib-inline			install
python3-mdurl					install
python3-mechanize				install
python3-minimal					install
python3-mpmath					install
python3-msgpack					install
python3-multiprocess				install
python3-mutagen					install
python3-nacl					install
python3-netaddr					install
python3-netifaces:amd64				install
python3-netplan					install
python3-numpy					install
python3-oauthlib				install
python3-packaging				install
python3-pam					install
python3-parso					install
python3-parted					install
python3-pexpect					install
python3-pikepdf					install
python3-pil:amd64				install
python3-pil.imagetk:amd64			install
python3-pkg-resources				install
python3-png					install
python3-problem-report				install
python3-prompt-toolkit				install
python3-psutil					install
python3-ptyprocess				install
python3-pure-eval				install
python3-py7zr					install
python3-pyasyncore				install
python3-pyatspi					install
python3-pyaudio					install
python3-pycryptodome				install
python3-pycurl					install
python3-pyelftools				install
python3-pygments				install
python3-pyinotify				install
python3-pyparsing				install
python3-pyqt5					install
python3-pyqt5.qtwebchannel			install
python3-pyqt5.qtwebengine			install
python3-pyqt5.sip				install
python3-pyqt6					install
python3-pyqt6.qtqml				install
python3-pyqt6.qtquick				install
python3-pyqt6.qtsvg				install
python3-pyqt6.qtwebchannel			install
python3-pyqt6.qtwebengine			install
python3-pyqt6.sip				install
python3-pyrsistent:amd64			install
python3-pyudev					install
python3-qrcode					install
python3-regex					install
python3-repolib					install
python3-repoze.lru				install
python3-requests				install
python3-requests-file				install
python3-rich					install
python3-routes					install
python3-samba					install
python3-scipy					install
python3-send2trash				install
python3-setproctitle:amd64			install
python3-setuptools				install
python3-sgmllib3k				install
python3-six					install
python3-soupsieve				install
python3-speechd					install
python3-stack-data				install
python3-sympy					install
python3-systemd					install
python3-talloc:amd64				install
python3-tdb					install
python3-texttable				install
python3-tinycss2				install
python3-tk:amd64				install
python3-tldextract				install
python3-traitlets				install
python3-typeshed				install
python3-typing-extensions			install
python3-tz					install
python3-ufolib2					install
python3-unicodedata2				install
python3-unidecode				install
python3-uno					install
python3-urllib3					install
python3-wadllib					install
python3-wcwidth					install
python3-webencodings				install
python3-webob					install
python3-websockets				install
python3-wrapt					install
python3-xapp					install
python3-xdg					install
python3-xkit					install
python3-xlib					install
python3-xlrd					install
python3-xxhash					install
python3-yaml					install
python3-zeroconf				install
python3.12					install
python3.12-minimal				install
qml-module-org-kde-bluezqt:amd64		install
qml-module-org-kde-kconfig:amd64		install
qml-module-org-kde-kirigami2			install
qml-module-org-kde-kquickcontrols:amd64		install
qml-module-org-kde-kquickcontrolsaddons:amd64	install
qml-module-org-kde-newstuff			install
qml-module-org-kde-prison:amd64			install
qml-module-org-kde-purpose:amd64		install
qml-module-qt-labs-folderlistmodel:amd64	install
qml-module-qt-labs-settings:amd64		install
qml-module-qtgraphicaleffects:amd64		install
qml-module-qtqml:amd64				install
qml-module-qtqml-models2:amd64			install
qml-module-qtquick-controls:amd64		install
qml-module-qtquick-controls2:amd64		install
qml-module-qtquick-dialogs:amd64		install
qml-module-qtquick-layouts:amd64		install
qml-module-qtquick-privatewidgets:amd64		install
qml-module-qtquick-templates2:amd64		install
qml-module-qtquick-window2:amd64		install
qml-module-qtquick2:amd64			install
qml-module-qtwebengine:amd64			install
qml-module-sso-onlineaccounts:amd64		install
qml-module-ubuntu-onlineaccounts		install
qt5-gtk-platformtheme:amd64			install
qt5-gtk2-platformtheme:amd64			install
qt5-style-plugin-cleanlooks:amd64		install
qt5-style-plugin-motif:amd64			install
qt5-style-plugin-plastique:amd64		install
qt5-style-plugins:amd64				install
qt6-gtk-platformtheme:amd64			install
qt6-image-formats-plugins			install
qt6-qpa-plugins:amd64				install
qt6-translations-l10n				install
qt6-wayland:amd64				install
qtspeech5-flite-plugin:amd64			install
qtspeech5-speechd-plugin:amd64			install
qttranslations5-l10n				install
qtwayland5:amd64				install
rake						install
rdate						install
readline-common					install
reiserfsprogs					install
rename						install
rfkill						install
rhythmbox					install
rhythmbox-data					install
rhythmbox-plugins				install
ristretto					install
rkhunter					install
rpcsvc-proto					install
rsync						install
rsyslog						install
rtkit						install
rubber						install
ruby						install
ruby-net-telnet					install
ruby-rubygems					install
ruby-sdbm:amd64					install
ruby-webrick					install
ruby-xmlrpc					install
ruby3.2						install
rubygems-integration				install
rygel						install
samba-common					install
samba-common-bin				install
samba-libs:amd64				install
sane-airscan					install
sane-utils					install
sbsigntool					install
seahorse					install
secureboot-db					install
sed						install
sensible-utils					install
session-migration				install
sgml-base					install
sgml-data					install
shared-mime-info				install
shim-signed					install
signon-plugin-oauth2				install
slick-greeter					install
smbclient					install
sonnet-plugins:amd64				install
sound-theme-freedesktop				install
speech-dispatcher				install
speech-dispatcher-audio-plugins:amd64		install
speech-dispatcher-espeak-ng			install
squashfs-tools					install
sse3-support					install
ssl-cert					install
strace						install
streamer					install
sudo						install
switcheroo-control				install
syslinux					install
syslinux-common					install
syslinux-utils					install
system-config-printer-common			install
system-config-printer-udev			install
system-tools-backends				install
systemd						install
systemd-coredump				install
systemd-dev					install
systemd-hwe-hwdb				install
systemd-resolved				install
systemd-sysv					install
systemd-timesyncd				install
sysvinit-utils					install
t1utils						install
tar						install
tcl						install
tcl8.6						install
tcpdump						install
teckit						install
tecla						install
telnet						install
tex-common					install
tex-gyre					install
texinfo						install
texinfo-lib					install
texlive						install
texlive-base					install
texlive-bibtex-extra				install
texlive-binaries				install
texlive-extra-utils				install
texlive-font-utils				install
texlive-fonts-extra				install
texlive-fonts-extra-doc				install
texlive-fonts-extra-links			install
texlive-fonts-recommended			install
texlive-fonts-recommended-doc			install
texlive-formats-extra				install
texlive-full					install
texlive-games					install
texlive-humanities				install
texlive-humanities-doc				install
texlive-lang-arabic				install
texlive-lang-chinese				install
texlive-lang-cjk				install
texlive-lang-cyrillic				install
texlive-lang-czechslovak			install
texlive-lang-english				install
texlive-lang-european				install
texlive-lang-french				install
texlive-lang-german				install
texlive-lang-greek				install
texlive-lang-italian				install
texlive-lang-japanese				install
texlive-lang-korean				install
texlive-lang-other				install
texlive-lang-polish				install
texlive-lang-portuguese				install
texlive-lang-spanish				install
texlive-latex-base				install
texlive-latex-base-doc				install
texlive-latex-extra				install
texlive-latex-extra-doc				install
texlive-latex-recommended			install
texlive-latex-recommended-doc			install
texlive-luatex					install
texlive-metapost				install
texlive-metapost-doc				install
texlive-music					install
texlive-pictures				install
texlive-pictures-doc				install
texlive-plain-generic				install
texlive-pstricks				install
texlive-pstricks-doc				install
texlive-publishers				install
texlive-publishers-doc				install
texlive-science					install
texlive-science-doc				install
texlive-xetex					install
texmaker					install
texmaker-data					install
texstudio					install
texworks					install
texworks-help-en				install
thermald					install
thingy						install
time						install
timgm6mb-soundfont				install
tipa						install
tk						install
tk8.6						install
tk8.6-blt2.5					install
tlp						deinstall
tlp-rdw						deinstall
tnftp						install
touchegg					install
tpm-udev					install
transmission-common				install
transmission-gtk				install
tumbler:amd64					install
tumbler-common					install
tzdata						install
tzdata-legacy					install
ubuntu-dbgsym-keyring				install
ubuntu-docs					install
ubuntu-drivers-common				install
ubuntu-kernel-accessories			install
ubuntu-keyring					install
ubuntu-mono					install
ubuntu-session					install
ubuntu-system-adjustments			install
ubuntu-wallpapers				install
ubuntu-wallpapers-noble				install
ucf						install
udev						install
udisks2						install
ufw						install
unhide						install
unhide.rb					install
unicode-data					install
uno-libs-private				install
unshield					install
untex						install
unzip						install
update-inetd					install
upower						install
ure						install
ure-java					install
usb-modeswitch					install
usb-modeswitch-data				install
usb.ids						install
usbguard					install
usbmuxd						install
usbutils					install
user-setup					install
util-linux					install
uuid-runtime					install
va-driver-all:amd64				install
vim-common					install
vim-tiny					install
vlc						install
vlc-bin						install
vlc-data					install
vlc-l10n					install
vlc-plugin-access-extra:amd64			install
vlc-plugin-base:amd64				install
vlc-plugin-notify:amd64				install
vlc-plugin-qt:amd64				install
vlc-plugin-samba:amd64				install
vlc-plugin-skins2:amd64				install
vlc-plugin-video-output:amd64			install
vlc-plugin-video-splitter:amd64			install
vlc-plugin-visualization:amd64			install
vprerex						install
vulkan-tools					install
wamerican					install
wbritish					install
wdutch						install
webp						install
webp-pixbuf-loader:amd64			install
wget						install
whiptail					install
whois						install
whoopsie					install
whoopsie-preferences				install
wireless-regdb					install
wireless-tools					install
wireplumber					install
wireshark					install
wireshark-common				install
wmctrl						install
wpasupplicant					install
x11-apps					install
x11-common					install
x11-session-utils				install
x11-utils					install
x11-xkb-utils					install
x11-xserver-utils				install
xapp-symbolic-icons				install
xapps-common					install
xauth						install
xawtv-plugins:amd64				install
xbitmaps					install
xbrlapi						install
xcvt						install
xdg-dbus-proxy					install
xdg-desktop-portal				install
xdg-desktop-portal-gtk				install
xdg-desktop-portal-xapp				install
xdg-user-dirs					install
xdg-user-dirs-gtk				install
xdg-utils					install
xed						install
xed-common					install
xfconf						install
xfonts-base					install
xfonts-encodings				install
xfonts-scalable					install
xfonts-utils					install
xfsprogs					install
xinit						install
xinput						install
xkb-data					install
xml-core					install
xorg						install
xorg-docs-core					install
xreader						install
xreader-common					install
xserver-common					install
xserver-xephyr					install
xserver-xorg					install
xserver-xorg-core				install
xserver-xorg-input-all				install
xserver-xorg-input-libinput			install
xserver-xorg-input-wacom			install
xserver-xorg-legacy				install
xserver-xorg-video-all				install
xserver-xorg-video-amdgpu			install
xserver-xorg-video-ati				install
xserver-xorg-video-fbdev			install
xserver-xorg-video-intel			install
xserver-xorg-video-nouveau			install
xserver-xorg-video-qxl				install
xserver-xorg-video-radeon			install
xserver-xorg-video-vesa				install
xserver-xorg-video-vmware			install
xterm						install
xwayland					install
xxd						install
xz-utils					install
yara						install
yaru-theme-gnome-shell				install
yaru-theme-icon					install
yelp						install
yelp-xsl					install
yt-dlp						install
zenity						install
zenity-common					install
zip						install
zlib1g:amd64					install
zlib1g:i386					install
zstd						install

---


# GEDAAN
    sudo apt update && sudo apt install qemu-system-x86 qemu-utils -y

```
root@mint:~# script /media/mint/USB-STAAFJE/terminal_log.txt
Script started, output log file is '/media/mint/USB-STAAFJE/terminal_log.txt'.
root@mint:~# ls -lh /media/mint/USB-STAAFJE/MINT_BACKUP/
total 72G
-rwxr-xr-x 1 mint mint  86K Jan 21 01:11 pakketlijst.txt
-rwxr-xr-x 1 mint mint 2.2M Jan 21 01:11 system_config.tar.gz
-rwxr-xr-x 1 mint mint  72G Jan 21 01:44 user_home_backup.tar.gz
root@mint:~# sudo apt update && sudo apt install qemu-system-x86 qemu-utils -y
Ign:1 cdrom://Linux Mint 22.3 _Zena_ - Release amd64 20260108 noble InRelease
Err:2 cdrom://Linux Mint 22.3 _Zena_ - Release amd64 20260108 noble Release
  Please use apt-cdrom to make this CD-ROM recognized by APT. apt-get update cannot be used to add new CD-ROMs
Get:3 http://security.ubuntu.com/ubuntu noble-security InRelease [126 kB]
Hit:4 http://archive.ubuntu.com/ubuntu noble InRelease                                                       
Get:5 http://archive.ubuntu.com/ubuntu noble-updates InRelease [126 kB]                                      
Get:6 http://archive.ubuntu.com/ubuntu noble-backports InRelease [126 kB]                                               
Ign:7 http://packages.linuxmint.com zena InRelease     
Get:8 http://packages.linuxmint.com zena Release [27.6 kB]
Get:9 http://security.ubuntu.com/ubuntu noble-security/main amd64 Packages [1408 kB]
Get:10 http://packages.linuxmint.com zena Release.gpg [833 B]
Get:11 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 Packages [1697 kB]       
Get:12 http://security.ubuntu.com/ubuntu noble-security/main i386 Packages [370 kB]
Get:13 http://security.ubuntu.com/ubuntu noble-security/main Translation-en [229 kB]       
Get:14 http://security.ubuntu.com/ubuntu noble-security/main amd64 Components [21.5 kB]         
Get:15 http://security.ubuntu.com/ubuntu noble-security/main amd64 c-n-f Metadata [9772 B]         
Get:16 http://security.ubuntu.com/ubuntu noble-security/restricted amd64 Packages [2302 kB]      
Get:17 http://security.ubuntu.com/ubuntu noble-security/restricted Translation-en [527 kB] 
Get:18 http://security.ubuntu.com/ubuntu noble-security/restricted amd64 Components [208 B]       
Get:19 http://security.ubuntu.com/ubuntu noble-security/universe amd64 Packages [924 kB]
Get:20 http://security.ubuntu.com/ubuntu noble-security/universe i386 Packages [572 kB]
Get:21 http://archive.ubuntu.com/ubuntu noble-updates/main i386 Packages [572 kB]
Get:22 http://archive.ubuntu.com/ubuntu noble-updates/main Translation-en [314 kB]         
Get:23 http://security.ubuntu.com/ubuntu noble-security/universe Translation-en [209 kB]                    
Get:24 http://security.ubuntu.com/ubuntu noble-security/universe amd64 Components [74.2 kB]                                  
Get:25 http://security.ubuntu.com/ubuntu noble-security/universe amd64 c-n-f Metadata [19.7 kB]                                 
Get:26 http://security.ubuntu.com/ubuntu noble-security/multiverse amd64 Components [208 B]                                    
Get:27 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 Components [175 kB]                        
Get:28 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 c-n-f Metadata [16.0 kB]
Get:29 http://archive.ubuntu.com/ubuntu noble-updates/restricted i386 Packages [24.2 kB]
Get:30 http://archive.ubuntu.com/ubuntu noble-updates/restricted amd64 Packages [2426 kB]
Get:31 http://archive.ubuntu.com/ubuntu noble-updates/restricted Translation-en [554 kB]
Get:32 http://archive.ubuntu.com/ubuntu noble-updates/restricted amd64 Components [212 B]
Get:33 http://archive.ubuntu.com/ubuntu noble-updates/universe i386 Packages [997 kB]
Get:34 http://archive.ubuntu.com/ubuntu noble-updates/universe amd64 Packages [1519 kB]
Get:35 http://archive.ubuntu.com/ubuntu noble-updates/universe Translation-en [310 kB]  
Get:36 http://archive.ubuntu.com/ubuntu noble-updates/universe amd64 Components [380 kB]     
Get:37 http://archive.ubuntu.com/ubuntu noble-updates/universe amd64 c-n-f Metadata [31.6 kB]   
Get:38 http://archive.ubuntu.com/ubuntu noble-updates/multiverse i386 Packages [7256 B]
Get:39 http://archive.ubuntu.com/ubuntu noble-updates/multiverse amd64 Packages [30.4 kB]
Get:40 http://archive.ubuntu.com/ubuntu noble-updates/multiverse amd64 Components [940 B]
Get:41 http://archive.ubuntu.com/ubuntu noble-backports/main amd64 Components [7300 B]        
Get:42 http://archive.ubuntu.com/ubuntu noble-backports/restricted amd64 Components [212 B]
Get:43 http://packages.linuxmint.com zena/main i386 Packages [17.9 kB]         
Get:44 http://archive.ubuntu.com/ubuntu noble-backports/universe amd64 Components [10.5 kB]
Get:45 http://archive.ubuntu.com/ubuntu noble-backports/multiverse amd64 Components [212 B]
Get:46 http://packages.linuxmint.com zena/main amd64 Packages [18.5 kB]
Get:47 http://packages.linuxmint.com zena/upstream amd64 Packages [50.3 kB]
Get:48 http://packages.linuxmint.com zena/upstream i386 Packages [19.5 kB]
Get:49 http://packages.linuxmint.com zena/backport i386 Packages [6404 B]
Get:50 http://packages.linuxmint.com zena/backport amd64 Packages [28.0 kB]
Reading package lists... Done                                
E: The repository 'cdrom://Linux Mint 22.3 _Zena_ - Release amd64 20260108 noble Release' does not have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
root@mint:~# exit
exit
Script done.
root@mint:~# 
```

# NOG NIET GEDAAN DUS
    sudo qemu-system-x86_64 -m 2048 -drive file=/dev/sda,format=raw,readonly=on -enable-kvm

---

# CONTROLE GEEFT
    tar -tvf /media/mint/USB-STAAFJE/MINT_BACKUP/system_config.tar.gz | head -n 10

```

root@mint:~# tar -tvf /media/mint/USB-STAAFJE/MINT_BACKUP/system_config.tar.gz | head -n 10
drwxr-xr-x root/root         0 2026-01-20 23:08 mnt/etc/
-rw-r--r-- root/root       119 2022-01-11 00:08 mnt/etc/catdocrc
drwxr-xr-x root/root         0 2026-01-10 00:10 mnt/etc/NetworkManager/
drwxr-xr-x root/root         0 2024-10-23 11:04 mnt/etc/NetworkManager/dnsmasq.d/
-rw-r--r-- root/root        98 2022-08-01 12:02 mnt/etc/NetworkManager/NetworkManager.conf
drwxr-xr-x root/root         0 2025-08-28 08:52 mnt/etc/NetworkManager/dispatcher.d/
drwxr-xr-x root/root         0 2024-10-23 11:04 mnt/etc/NetworkManager/dispatcher.d/pre-down.d/
drwxr-xr-x root/root         0 2024-10-23 11:04 mnt/etc/NetworkManager/dispatcher.d/no-wait.d/
drwxr-xr-x root/root         0 2024-10-23 11:04 mnt/etc/NetworkManager/dispatcher.d/pre-up.d/
drwxr-xr-x root/root         0 2024-10-23 11:04 mnt/etc/NetworkManager/VPN/
root@mint:~# tar -tvf /media/mint/USB-STAAFJE/MINT_BACKUP/system_config.tar.gz | head -n 50
drwxr-xr-x root/root         0 2026-01-20 23:08 mnt/etc/
-rw-r--r-- root/root       119 2022-01-11 00:08 mnt/etc/catdocrc
drwxr-xr-x root/root         0 2026-01-10 00:10 mnt/etc/NetworkManager/
drwxr-xr-x root/root         0 2024-10-23 11:04 mnt/etc/NetworkManager/dnsmasq.d/
-rw-r--r-- root/root        98 2022-08-01 12:02 mnt/etc/NetworkManager/NetworkManager.conf
drwxr-xr-x root/root         0 2025-08-28 08:52 mnt/etc/NetworkManager/dispatcher.d/
drwxr-xr-x root/root         0 2024-10-23 11:04 mnt/etc/NetworkManager/dispatcher.d/pre-down.d/
drwxr-xr-x root/root         0 2024-10-23 11:04 mnt/etc/NetworkManager/dispatcher.d/no-wait.d/
drwxr-xr-x root/root         0 2024-10-23 11:04 mnt/etc/NetworkManager/dispatcher.d/pre-up.d/
drwxr-xr-x root/root         0 2024-10-23 11:04 mnt/etc/NetworkManager/VPN/
drwxr-xr-x root/root         0 2025-12-16 20:11 mnt/etc/NetworkManager/system-connections/
drwxr-xr-x root/root         0 2026-01-13 20:25 mnt/etc/NetworkManager/conf.d/
-rw-r--r-- root/root        32 2022-08-01 12:02 mnt/etc/NetworkManager/conf.d/default-wifi-powersave-on.conf
-rw-r--r-- root/root        31 2025-12-11 15:33 mnt/etc/NetworkManager/conf.d/20-connectivity-disable.conf
-rw-r--r-- root/root        33 2024-07-27 12:57 mnt/etc/NetworkManager/conf.d/ubuntu-system-adjustments.conf
drwxr-xr-x root/root         0 2024-10-23 11:04 mnt/etc/NetworkManager/dnsmasq-shared.d/
drwxr-xr-x root/root         0 2026-01-18 00:17 mnt/etc/dpkg/
-rw-r--r-- root/root       260 2024-09-26 19:14 mnt/etc/dpkg/shlibs.default
-rw-r--r-- root/root       253 2024-09-26 19:14 mnt/etc/dpkg/shlibs.override
drwxr-xr-x root/root         0 2026-01-12 12:54 mnt/etc/dpkg/origins/
lrwxrwxrwx root/root         0 2025-11-23 20:24 mnt/etc/dpkg/origins/default -> ubuntu
-rw-r--r-- root/root       114 2024-04-22 13:04 mnt/etc/dpkg/origins/ubuntu
-rw-r--r-- root/root        83 2024-04-22 13:04 mnt/etc/dpkg/origins/debian
drwxr-xr-x root/root         0 2026-01-16 01:09 mnt/etc/dpkg/dpkg.cfg.d/
-rw-r--r-- root/root       274 2024-12-05 11:53 mnt/etc/dpkg/dpkg.cfg.d/needrestart
-rw-r--r-- root/root       446 2023-02-14 22:56 mnt/etc/dpkg/dpkg.cfg
-rw-r--r-- root/root       411 2025-08-28 08:52 mnt/etc/hosts.allow
-rwxr-xr-x root/root     16593 2026-01-13 20:21 mnt/etc/nftables.conf
drwxr-xr-x root/dip          0 2025-08-28 08:52 mnt/etc/ppp/
-rwxr-xr-x root/root       834 2022-08-18 12:54 mnt/etc/ppp/ipv6-down
drwxr-xr-x root/root         0 2024-04-03 17:56 mnt/etc/ppp/ipv6-up.d/
-rw------- root/root        80 2025-08-28 08:52 mnt/etc/ppp/chap-secrets
-rwxr-xr-x root/root      1898 2022-08-18 12:54 mnt/etc/ppp/ip-up
drwxr-xr-x root/root         0 2024-04-03 17:56 mnt/etc/ppp/ip-pre-up.d/
drwxr-xr-x root/root         0 2026-01-15 11:09 mnt/etc/ppp/ip-down.d/
-rwxr-xr-x root/root       718 2022-08-18 12:54 mnt/etc/ppp/ip-down.d/0000usepeerdns
-rwxr-xr-x root/root       802 2024-04-08 14:48 mnt/etc/ppp/ip-down.d/postfix
-rwxr-xr-x root/root      2608 2025-06-13 08:02 mnt/etc/ppp/ip-down.d/clamav-freshclam-ifupdown
-rwxr-xr-x root/root       974 2022-08-18 12:54 mnt/etc/ppp/ipv6-up
drwxr-xr-x root/root         0 2026-01-15 11:09 mnt/etc/ppp/ip-up.d/
-rwxr-xr-x root/root      1176 2022-08-18 13:06 mnt/etc/ppp/ip-up.d/0000usepeerdns
-rwxr-xr-x root/root      1185 2024-04-08 14:48 mnt/etc/ppp/ip-up.d/postfix
-rwxr-xr-x root/root      2608 2025-06-13 08:02 mnt/etc/ppp/ip-up.d/clamav-freshclam-ifupdown
-rw------- root/root      1628 2025-08-28 08:52 mnt/etc/ppp/pap-secrets
-rwxr-xr-x root/root      1757 2022-08-18 12:54 mnt/etc/ppp/ip-down
-rw-r--r-- root/root      2151 2024-04-08 16:16 mnt/etc/ppp/options.pptp
drwxr-s--- root/dip          0 2025-08-28 08:52 mnt/etc/ppp/peers/
-rw-r----- root/dip       1093 2025-08-28 08:52 mnt/etc/ppp/peers/provider
drwxr-xr-x root/root         0 2024-04-03 17:56 mnt/etc/ppp/ipv6-down.d/
-rw-r--r-- root/root     13209 2022-08-18 12:54 mnt/etc/ppp/options
root@mint:~# 

```

---

# OPSEC

```
root@mint:~# sudo find /mnt -xdev -not -path '*/.*' > /media/mint/USB-STAAFJE/MINT_BACKUP/volledige_bestandslijst.txt
root@mint:~# {
  echo "=== CUSTOM FIREWALL RULES (UFW) ==="
  sudo cat /mnt/etc/ufw/user.rules
  echo -e "\n=== KERNEL HARDENING (SYSCTL) ==="
  sudo cat /mnt/etc/sysctl.conf /mnt/etc/sysctl.d/*.conf
  echo -e "\n=== HOSTS & NETWERK ==="
  sudo cat /mnt/etc/hosts
  echo -e "\n=== CRON JOBS (CUSTOM SCRIPTS) ==="
  sudo ls -R /mnt/etc/cron.* echo -e "\n=== SSH CONFIG ==="
  sudo cat /mnt/etc/ssh/sshd_config
  echo -e "\n=== LOGS & AUDITD (IF INSTALLED) ==="
  sudo ls -l /mnt/etc/audit/rules.d/
} > /media/mint/USB-STAAFJE/MINT_BACKUP/custom_opsec_rules_index.txt
ls: invalid option -- 'e'
Try 'ls --help' for more information.
cat: /mnt/etc/ssh/sshd_config: No such file or directory
root@mint:~# 
```

# OPSEC

```
=== CUSTOM FIREWALL RULES (UFW) ===
*filter
:ufw-user-input - [0:0]
:ufw-user-output - [0:0]
:ufw-user-forward - [0:0]
:ufw-before-logging-input - [0:0]
:ufw-before-logging-output - [0:0]
:ufw-before-logging-forward - [0:0]
:ufw-user-logging-input - [0:0]
:ufw-user-logging-output - [0:0]
:ufw-user-logging-forward - [0:0]
:ufw-after-logging-input - [0:0]
:ufw-after-logging-output - [0:0]
:ufw-after-logging-forward - [0:0]
:ufw-logging-deny - [0:0]
:ufw-logging-allow - [0:0]
:ufw-user-limit - [0:0]
:ufw-user-limit-accept - [0:0]
### RULES ###

### tuple ### allow any 53 0.0.0.0/0 any 0.0.0.0/0 out
-A ufw-user-output -p tcp --dport 53 -j ACCEPT
-A ufw-user-output -p udp --dport 53 -j ACCEPT

### tuple ### allow tcp 80 0.0.0.0/0 any 0.0.0.0/0 out
-A ufw-user-output -p tcp --dport 80 -j ACCEPT

### tuple ### allow any 443 0.0.0.0/0 any 0.0.0.0/0 out
-A ufw-user-output -p tcp --dport 443 -j ACCEPT
-A ufw-user-output -p udp --dport 443 -j ACCEPT

### tuple ### allow udp 67 0.0.0.0/0 any 0.0.0.0/0 out
-A ufw-user-output -p udp --dport 67 -j ACCEPT

### tuple ### allow udp 68 0.0.0.0/0 any 0.0.0.0/0 out
-A ufw-user-output -p udp --dport 68 -j ACCEPT

### tuple ### deny udp 5353 0.0.0.0/0 any 0.0.0.0/0 out
-A ufw-user-output -p udp --dport 5353 -j DROP

### tuple ### deny udp 5353 0.0.0.0/0 any 0.0.0.0/0 in
-A ufw-user-input -p udp --dport 5353 -j DROP

### tuple ### deny udp 1900 0.0.0.0/0 any 0.0.0.0/0 out
-A ufw-user-output -p udp --dport 1900 -j DROP

### tuple ### deny udp 1900 0.0.0.0/0 any 0.0.0.0/0 in
-A ufw-user-input -p udp --dport 1900 -j DROP

### END RULES ###

### LOGGING ###
-A ufw-after-logging-input -j LOG --log-prefix "[UFW BLOCK] " -m limit --limit 3/min --limit-burst 10
-A ufw-after-logging-forward -j LOG --log-prefix "[UFW BLOCK] " -m limit --limit 3/min --limit-burst 10
-I ufw-logging-deny -m conntrack --ctstate INVALID -j RETURN -m limit --limit 3/min --limit-burst 10
-A ufw-logging-deny -j LOG --log-prefix "[UFW BLOCK] " -m limit --limit 3/min --limit-burst 10
-A ufw-logging-allow -j LOG --log-prefix "[UFW ALLOW] " -m limit --limit 3/min --limit-burst 10
### END LOGGING ###

### RATE LIMITING ###
-A ufw-user-limit -m limit --limit 3/minute -j LOG --log-prefix "[UFW LIMIT BLOCK] "
-A ufw-user-limit -j REJECT
-A ufw-user-limit-accept -j ACCEPT
### END RATE LIMITING ###
COMMIT

=== KERNEL HARDENING (SYSCTL) ===
#
# /etc/sysctl.conf - Configuration file for setting system variables
# See /etc/sysctl.d/ for additional system variables.
# See sysctl.conf (5) for information.
#

#kernel.domainname = example.com

# Uncomment the following to stop low-level messages on console
#kernel.printk = 3 4 1 3

###################################################################
# Functions previously found in netbase
#

# Uncomment the next two lines to enable Spoof protection (reverse-path filter)
# Turn on Source Address Verification in all interfaces to
# prevent some spoofing attacks
#net.ipv4.conf.default.rp_filter=1
#net.ipv4.conf.all.rp_filter=1

# Uncomment the next line to enable TCP/IP SYN cookies
# See http://lwn.net/Articles/277146/
# Note: This may impact IPv6 TCP sessions too
#net.ipv4.tcp_syncookies=1

# Uncomment the next line to enable packet forwarding for IPv4
#net.ipv4.ip_forward=1

# Uncomment the next line to enable packet forwarding for IPv6
#  Enabling this option disables Stateless Address Autoconfiguration
#  based on Router Advertisements for this host
#net.ipv6.conf.all.forwarding=1


###################################################################
# Additional settings - these settings can improve the network
# security of the host and prevent against some network attacks
# including spoofing attacks and man in the middle attacks through
# redirection. Some network environments, however, require that these
# settings are disabled so review and enable them as needed.
#
# Do not accept ICMP redirects (prevent MITM attacks)
#net.ipv4.conf.all.accept_redirects = 0
#net.ipv4.conf.default.accept_redirects = 0
# _or_
# Accept ICMP redirects only for gateways listed in our default
# gateway list (enabled by default)
# net.ipv4.conf.all.secure_redirects = 1
#
# Do not send ICMP redirects (we are not a router)
#net.ipv4.conf.all.send_redirects = 0
#
# Log Martian Packets
#net.ipv4.conf.all.log_martians = 1
#

###################################################################
# Magic system request Key
# 0=disable, 1=enable all, >1 bitmask of sysrq functions
# See https://www.kernel.org/doc/html/latest/admin-guide/sysrq.html
# for what other values do
#kernel.sysrq=438

# The Fair Queue CoDel packet scheduler is an across the board improvement to
# the default pfifo_fast qdisc. It reduces bottleneck delays, provides accurate
# RTT estimates to elephant TCP flows, and still allows shorter (sparser) flows
# like DNS, ARP, SYN, routing, etc packets priority access. For technical
# details, refer to https://www.bufferbloat.net/projects/codel/wiki/
#
# To fight bufferbloat, set it as the default qdisc in Ubuntu.
-net.core.default_qdisc = fq_codel

# the following stops low-level messages on console
kernel.printk = 4 4 1 7
# IPv6 Privacy Extensions (RFC 4941)
# ---
# IPv6 typically uses a device's MAC address when choosing an IPv6 address
# to use in autoconfiguration. Privacy extensions allow using a randomly
# generated IPv6 address, which increases privacy.
#
# Acceptable values:
#    0 - don’t use privacy extensions.
#    1 - generate privacy addresses
#    2 - prefer privacy addresses and use them over the normal addresses.
net.ipv6.conf.all.use_tempaddr = 2
net.ipv6.conf.default.use_tempaddr = 2
# These settings are specific to hardening the kernel itself from attack
# from userspace, rather than protecting userspace from other malicious
# userspace things.
#
#
# When an attacker is trying to exploit the local kernel, it is often
# helpful to be able to examine where in memory the kernel, modules,
# and data structures live. As such, kernel addresses should be treated
# as sensitive information.
#
# Many files and interfaces contain these addresses (e.g. /proc/kallsyms,
# /proc/modules, etc), and this setting can censor the addresses. A value
# of "0" allows all users to see the kernel addresses. A value of "1"
# limits visibility to the root user, and "2" blocks even the root user.
kernel.kptr_restrict = 1

# Access to the kernel log buffer can be especially useful for an attacker
# attempting to exploit the local kernel, as kernel addresses and detailed
# call traces are frequently found in kernel oops messages. Setting
# dmesg_restrict to "0" allows all users to view the kernel log buffer,
# and setting it to "1" restricts access to those with CAP_SYSLOG.
#
# dmesg_restrict defaults to 1 via CONFIG_SECURITY_DMESG_RESTRICT, only
# uncomment the following line to disable.
# kernel.dmesg_restrict = 0
# The magic SysRq key enables certain keyboard combinations to be
# interpreted by the kernel to help with debugging. The kernel will respond
# to these keys regardless of the current running applications.
#
# In general, the magic SysRq key is not needed for the average Ubuntu
# system, and having it enabled by default can lead to security issues on
# the console such as being able to dump memory or to kill arbitrary
# processes including the running screen lock.
#
# Here is the list of possible values:
#   0 - disable sysrq completely
#   1 - enable all functions of sysrq
#  >1 - enable certain functions by adding up the following values:
#          2 - enable control of console logging level
#          4 - enable control of keyboard (SAK, unraw)
#          8 - enable debugging dumps of processes etc.
#         16 - enable sync command
#         32 - enable remount read-only
#         64 - enable signalling of processes (term, kill, oom-kill)
#        128 - allow reboot/poweroff
#        256 - allow nicing of all RT tasks
#
#   For example, to enable both control of console logging level and
#   debugging dumps of processes: kernel.sysrq = 10
#
kernel.sysrq = 176
# Increase the number of virtual memory areas that one process may request
# https://bugs.launchpad.net/ubuntu/+source/procps/+bug/2057792
vm.max_map_count=1048576

# Turn on Source Address Verification in all interfaces to
# prevent some spoofing attacks.
net.ipv4.conf.default.rp_filter=2
net.ipv4.conf.all.rp_filter=2

# The PTRACE system is used for debugging.  With it, a single user process
# can attach to any other dumpable process owned by the same user.  In the
# case of malicious software, it is possible to use PTRACE to access
# credentials that exist in memory (re-using existing SSH connections,
# extracting GPG agent information, etc).
#
# A PTRACE scope of "0" is the more permissive mode.  A scope of "1" limits
# PTRACE only to direct child processes (e.g. "gdb name-of-program" and
# "strace -f name-of-program" work, but gdb's "attach" and "strace -fp $PID"
# do not).  The PTRACE scope is ignored when a user has CAP_SYS_PTRACE, so
# "sudo strace -fp $PID" will work as before.  For more details see:
# https://wiki.ubuntu.com/SecurityTeam/Roadmap/KernelHardening#ptrace
#
# For applications launching crash handlers that need PTRACE, exceptions can
# be registered by the debugee by declaring in the segfault handler
# specifically which process will be using PTRACE on the debugee:
#   prctl(PR_SET_PTRACER, debugger_pid, 0, 0, 0);
#
# In general, PTRACE is not needed for the average running Ubuntu system.
# To that end, the default is to set the PTRACE scope to "1".  This value
# may not be appropriate for developers or servers with only admin accounts.
kernel.yama.ptrace_scope = 1
# Protect the zero page of memory from userspace mmap to prevent kernel
# NULL-dereference attacks against potential future kernel security
# vulnerabilities.  (Added in kernel 2.6.23.)
#
# While this default is built into the Ubuntu kernel, there is no way to
# restore the kernel default if the value is changed during runtime; for
# example via package removal (e.g. wine, dosemu).  Therefore, this value
# is reset to the secure default each time the sysctl values are loaded.
vm.mmap_min_addr = 65536
# Allow the use of unprivileged user namespaces
# See https://github.com/linuxmint/mint22-beta/issues/82.
kernel.apparmor_restrict_unprivileged_userns = 0


# Voorkom informatielekken via dmesg
kernel.dmesg_restrict = 1

# Beperk toegang tot kernel symbols (voorkomt exploits)
kernel.kptr_restrict = 2

# Verhoog bescherming tegen 'buffer overflow' aanvallen
kernel.randomize_va_space = 2

# Bescherming tegen IP-spoofing (Source routing uitschakelen)
net.ipv4.conf.all.accept_source_route = 0
net.ipv4.conf.default.accept_source_route = 0

# Schakel redirects uit (voorkomt MITM aanvallen)
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.default.accept_redirects = 0

kernel.randomize_va_space=2
kernel.yama.ptrace_scope=1
kernel.kptr_restrict=2
kernel.dmesg_restrict=1
kernel.kptr_restrict=2
kernel.dmesg_restrict=1
#
# /etc/sysctl.conf - Configuration file for setting system variables
# See /etc/sysctl.d/ for additional system variables.
# See sysctl.conf (5) for information.
#

#kernel.domainname = example.com

# Uncomment the following to stop low-level messages on console
#kernel.printk = 3 4 1 3

###################################################################
# Functions previously found in netbase
#

# Uncomment the next two lines to enable Spoof protection (reverse-path filter)
# Turn on Source Address Verification in all interfaces to
# prevent some spoofing attacks
#net.ipv4.conf.default.rp_filter=1
#net.ipv4.conf.all.rp_filter=1

# Uncomment the next line to enable TCP/IP SYN cookies
# See http://lwn.net/Articles/277146/
# Note: This may impact IPv6 TCP sessions too
#net.ipv4.tcp_syncookies=1

# Uncomment the next line to enable packet forwarding for IPv4
#net.ipv4.ip_forward=1

# Uncomment the next line to enable packet forwarding for IPv6
#  Enabling this option disables Stateless Address Autoconfiguration
#  based on Router Advertisements for this host
#net.ipv6.conf.all.forwarding=1


###################################################################
# Additional settings - these settings can improve the network
# security of the host and prevent against some network attacks
# including spoofing attacks and man in the middle attacks through
# redirection. Some network environments, however, require that these
# settings are disabled so review and enable them as needed.
#
# Do not accept ICMP redirects (prevent MITM attacks)
#net.ipv4.conf.all.accept_redirects = 0
#net.ipv4.conf.default.accept_redirects = 0
# _or_
# Accept ICMP redirects only for gateways listed in our default
# gateway list (enabled by default)
# net.ipv4.conf.all.secure_redirects = 1
#
# Do not send ICMP redirects (we are not a router)
#net.ipv4.conf.all.send_redirects = 0
#
# Log Martian Packets
#net.ipv4.conf.all.log_martians = 1
#

###################################################################
# Magic system request Key
# 0=disable, 1=enable all, >1 bitmask of sysrq functions
# See https://www.kernel.org/doc/html/latest/admin-guide/sysrq.html
# for what other values do
#kernel.sysrq=438

# --- NETWORK STACK HARDENING ---

# IP Spoofing protection (Strict mode)
net.ipv4.conf.all.rp_filter = 1
net.ipv4.conf.default.rp_filter = 1

# Ignore ICMP Broadcasts (Anti-Smurf/Ping Flood)
net.ipv4.icmp_echo_ignore_broadcasts = 1

# Disable Source Packet Routing (Geen router spelen)
net.ipv4.conf.all.accept_source_route = 0
net.ipv6.conf.all.accept_source_route = 0
net.ipv4.conf.default.accept_source_route = 0
net.ipv6.conf.default.accept_source_route = 0

# Disable Redirects (Voorkomt Man-in-the-Middle hijacking)
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.default.accept_redirects = 0
net.ipv6.conf.all.accept_redirects = 0
net.ipv6.conf.default.accept_redirects = 0
net.ipv4.conf.all.secure_redirects = 0
net.ipv4.conf.default.secure_redirects = 0

# TCP Hardening (SYN Flood protection & Time-Wait Assassination)
net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_rfc1337 = 1

# Log Martians (Detectie van spoofed packets)
net.ipv4.conf.all.log_martians = 1

# --- KERNEL SECURITY (ANTI-EXPLOIT) ---

# PTRACE Scope: Blokkeer process spying. 
# Voorkomt dat malware in browser processen kan injecteren of memory kan lezen.
kernel.yama.ptrace_scope = 2

# Dmesg Restrict: Verberg kernel adressen voor normale gebruikers.
# Maakt het véél moeilijker om exploits te schrijven die afhankelijk zijn van memory layout.
kernel.dmesg_restrict = 1

# BPF Hardening: JIT compiler hardening voor eBPF (vaak misbruikt)
net.core.bpf_jit_harden = 2
kernel.unprivileged_bpf_disabled = 1

# Kexec Disable: Voorkomt het laden van een nieuwe kernel tijdens runtime (Rootkit preventie)
kernel.kexec_load_disabled = 1

# ASLR (Address Space Layout Randomization) maximaliseren
kernel.randomize_va_space = 2

# Magic SysRq key uitschakelen (Fysieke access hardening)
kernel.sysrq = 0

kernel.kptr_restrict=2
kernel.sysrq=0
kernel.unprivileged_bpf_disabled=1
net.core.bpf_jit_harden=2
dev.tty.ldisc_autoload=0
vm.unprivileged_userfaultfd=0
kernel.perf_event_paranoid=3
fs.suid_dumpable = 0
fs.protected_fifos = 2
fs.protected_regular = 2
fs.protected_hardlinks = 1
fs.protected_symlinks = 1
dev.tty.ldisc_autoload = 0
fs.inotify.max_user_watches = 524288
fs.protected_fifos = 2
fs.protected_regular = 2
fs.protected_hardlinks = 1
fs.protected_symlinks = 1
dev.tty.ldisc_autoload = 0
fs.inotify.max_user_watches = 524288
kernel.io_delay_type = 3
kernel.unprivileged_userns_clone=0
kernel.modules_disabled = 1

=== HOSTS & NETWERK ===
127.0.0.1	localhost
127.0.1.1	MSI-DESKTOP

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters

=== CRON JOBS (CUSTOM SCRIPTS) ===

=== LOGS & AUDITD (IF INSTALLED) ===
total 8
-rw------- 1 root root   5 Jan 16 02:58 99-finalize.rules
-rw-r----- 1 root root 249 Jan 16 01:40 audit.rules

---

```





