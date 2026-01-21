**SITREP:**
Dit is een **MASS RESTORATION PROTOCOL**.
De lijst die je geeft is het exacte formaat van `dpkg --get-selections`.
We gaan een script bouwen dat deze lijst parsed, de packages die gemarkeerd staan als `install` installeert, en de packages die gemarkeerd staan als `deinstall` (zoals `dkms` en `tlp` in jouw lijst) verwijdert.

**INSTRUCTIES VOOR DE OPERATOR:**

1. Kopieer jouw **hele lijst** hierboven.
2. Maak een tekstbestand op je **Bureaublad** (Desktop) genaamd: `restore_list.txt`.
3. Plak de lijst erin en sla op.
4. Draai onderstaand script.

---

### HET SCRIPT: `deploy_packages.sh`

Dit script leest de file, filtert de acties, en voert ze uit met `apt`.

```bash
#!/bin/bash
# -----------------------------------------------------------------------
# OPERATION: MASS PACKAGE RESTORATION
# TARGET:    Linux Mint / Debian based systems
# INPUT:     ~/Desktop/restore_list.txt (dpkg selection format)
# AUTHOR:    YOURI SLOT / GEMINI PRO
# -----------------------------------------------------------------------

# 1. DEFINIEER VARIABELEN
INPUT_FILE="$HOME/Desktop/restore_list.txt"
LOG_FILE="$HOME/Desktop/install_log.txt"

# 2. CHECK ROOT
if [[ $EUID -ne 0 ]]; then
   echo "[!] ERROR: DIT SCRIPT MOET ALS ROOT DRAAIEN."
   echo "    COMMENCE: sudo $0"
   exit 1
fi

# 3. CHECK INPUT FILE
if [ ! -f "$INPUT_FILE" ]; then
    echo "[!] ERROR: BESTAND NIET GEVONDEN OP: $INPUT_FILE"
    echo "    Maak het bestand aan en plak de lijst erin."
    exit 1
fi

echo "[*] INITIATING PACKAGE DEPLOYMENT..."
echo "[*] LOGGING TO: $LOG_FILE"

# 4. UPDATE REPOSITORIES (CRITICAL)
echo "[+] UPDATING REPO CACHE..."
apt-get update -y

# 5. PARSE EN INSTALL ('install' gemarkeerd)
echo "[+] PARSING INSTALL LIST..."
# We gebruiken awk om alleen de eerste kolom te pakken ALS de tweede kolom 'install' is.
# We gebruiken xargs om de lijst aan apt te voeren (voorkomt 'argument too long').
awk '$2 == "install" {print $1}' "$INPUT_FILE" | xargs apt-get install -y --ignore-missing >> "$LOG_FILE" 2>&1

if [ $? -eq 0 ]; then
    echo "[V] INSTALL PHASE COMPLETE."
else
    echo "[!] WARNING: ERRORS DETECTED DURING INSTALL. CHECK LOG."
fi

# 6. PARSE EN REMOVE ('deinstall' gemarkeerd)
# In jouw lijst staan 'dkms' en 'tlp' op deinstall. Dit voert dat uit.
echo "[+] PARSING REMOVAL LIST..."
awk '$2 == "deinstall" {print $1}' "$INPUT_FILE" | xargs apt-get remove -y --purge >> "$LOG_FILE" 2>&1

echo "[*] CLEANING UP..."
apt-get autoremove -y >> "$LOG_FILE" 2>&1

echo "-----------------------------------------------------"
echo "   OPERATION COMPLETE."
echo "   SYSTEM STATE RESTORED PER LIST."
echo "   CHECK $LOG_FILE FOR DETAILS."
echo "-----------------------------------------------------"

```

### UITVOEREN

Open Terminal in de map waar je het script hebt opgeslagen:

```bash
chmod +x deploy_packages.sh
sudo ./deploy_packages.sh

```
