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
