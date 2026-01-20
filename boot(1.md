Om Boot Repair toegang te geven tot je versleutelde bestanden, moet je de container 'mappen' (openen) en de logische volumes activeren.

### PAYLOAD: UNLOCK & MOUNT LUKS

Voer deze regels regel voor regel uit in de terminal.

```bash
# 1. ZOEK JE VERSLEUTELDE PARTITIE
# Zoek de grootste partitie, waarschijnlijk sda3 of nvme0n1p3.
lsblk

# 2. OPEN DE CONTAINER (DECRYPTIE)
# Vervang /dev/sdXY door jouw encrypted partitie (bv. /dev/sda3)
# 'cryptdata' is de naam die we het tijdelijk geven.
sudo cryptsetup open /dev/sdXY cryptdata
# (Voer je wachtwoord in als erom gevraagd wordt)

# 3. ACTIVEER LVM (CRUCIAAL BIJ MINT)
# Mint gebruikt standaard LVM binnenin de encryptie.
# Dit commando scant en activeert de volumes (zoals 'root' en 'swap').
sudo vgchange -ay

# 4. CONTROLEER DE MAPPER PADEN
# Kijk nu hoe de volumes heten onder de 'cryptdata' tak.
lsblk
# Je zoekt iets als: /dev/mapper/vgmint-root of /dev/mapper/mint--vg-root

# 5. MOUNT DE ROOT PARTITIE
# Vervang het pad hieronder met wat je bij stap 4 vond.
sudo mount /dev/mapper/vgmint-root /mnt

# 6. MOUNT DE BOOT PARTITIE (Indien apart)
# Boot Repair heeft vaak ook de /boot partitie nodig.
# Dit is vaak de partitie direct boven je encrypted partitie (bv sda2).
sudo mount /dev/sdXZ /mnt/boot

# NU KAN JE BOOT REPAIR STARTEN

```

**Next Step:**
Als `lsblk` na stap 2 of 3 geen logische volumes (zoals `root`) laat zien, plak dan hier de output van `lsblk`, dan is de structuur anders (geen LVM).
