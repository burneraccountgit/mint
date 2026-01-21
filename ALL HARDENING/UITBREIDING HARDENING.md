**BEGREPEN. OPERATOR SEARCH INDEX GEGENEREERD.**

HIERONDER DE DIRECTE REFERENTIES. GEBRUIK `CTRL+F` EN ZOEK OP DEZE TAGS OM JE CODE TE PAKKEN.

---

### **KEYWORD: INSTALL_MANUAL**

*(Fysieke Handelingen - VOOR SCRIPTING)*

1. **BIOS/UEFI:**
* **SECURE BOOT:** [ AAN ]
* **FAST BOOT:** [ UIT ]
* **TPM:** [ AAN ]


2. **FYSIEK:**
* **NETWERKKABEL:** [ LOSKOPPELEN ] (100% Offline installatie).


3. **PARTITIONERING (CRITIQUE):**
* Kies: *"Erase disk and install Linux Mint"*.
* Klik: *"Advanced Features"*.
* Selecteer: **"Use LVM with the new Linux Mint installation"**.
* Selecteer: **"Encrypt the new Linux Mint installation for security"**.



---

### **KEYWORD: BUNKER_SETUP**

*(Script 1: Hardening & Firewall - NA EERSTE REBOOT - OPSLAAN ALS `bunker_setup.sh`)*

```bash
#!/bin/bash
# KEYWORD: BUNKER_SETUP
# DOEL: FIREWALL LOCKDOWN & BASIC TOOLS (GEEN KERNEL MODS)

if [[ $EUID -ne 0 ]]; then
   echo "Run as root: sudo $0"
   exit 1
fi

echo "[*] BUNKER PROTOCOL INITIATED..."

# 1. BASE UPDATE
apt-get update && apt-get upgrade -y

# 2. FIREWALL LOCKDOWN
ufw default deny incoming
ufw default allow outgoing
ufw enable
echo "[V] FIREWALL ACTIVE."

# 3. TOOLCHAIN DEPLOYMENT
apt-get install -y poppler-utils tesseract-ocr tesseract-ocr-nld git curl keepassxc mat2 ripgrep

# 4. SERVICES
systemctl disable bluetooth
echo "[V] BLUETOOTH KILLED."

echo "[*] BUNKER SETUP COMPLETE."

```

*Uitvoeren:* `chmod +x bunker_setup.sh` -> `sudo ./bunker_setup.sh`

---

### **KEYWORD: RESTORE_LIST**

*(De Data voor Script 2)*

1. Maak een bestand op je **Desktop** genaamd: `restore_list.txt`.
2. **PLAK** daar jouw volledige lijst in (die begint met `7zip install` en eindigt met `zstd install`).
3. Sla op.

---

### **KEYWORD: DEPLOY_PACKAGES**

*(Script 2: Bulk Installer - OPSLAAN ALS `deploy_packages.sh`)*

```bash
#!/bin/bash
# KEYWORD: DEPLOY_PACKAGES
# DOEL: LEEST 'restore_list.txt' EN INSTALLEERT ALLES

INPUT_FILE="$HOME/Desktop/restore_list.txt"

if [[ $EUID -ne 0 ]]; then
   echo "Run as root: sudo $0"
   exit 1
fi

if [ ! -f "$INPUT_FILE" ]; then
    echo "ERROR: $INPUT_FILE NIET GEVONDEN."
    exit 1
fi

echo "[*] STARTING MASS INSTALL..."
apt-get update -y

# INSTALLATIE LOOP
awk '$2 == "install" {print $1}' "$INPUT_FILE" | xargs apt-get install -y --ignore-missing

# SCHOONMAAK LOOP ('deinstall' items verwijderen)
awk '$2 == "deinstall" {print $1}' "$INPUT_FILE" | xargs apt-get remove -y --purge

echo "[V] DEPLOYMENT COMPLETE."

```

*Uitvoeren:* `chmod +x deploy_packages.sh` -> `sudo ./deploy_packages.sh`

---

### **KEYWORD: GRIND_EVIDENCE**

*(Script 3: PDF naar Source Code - OPSLAAN IN `_RAID_DUMP` MAP)*

```bash
#!/bin/bash
# KEYWORD: GRIND_EVIDENCE
# DOEL: ALLE PDFS IN DE MAP OMZETTEN NAAR TXT

mkdir -p ./00_GRIND_OUTPUT

for pdf_file in *.pdf; do
    [ -e "$pdf_file" ] || continue
    
    base_name=$(basename "$pdf_file" .pdf)
    output_file="./00_GRIND_OUTPUT/SRC_${base_name}.txt"
    
    echo "PROCESSING: $pdf_file"
    pdftotext -layout "$pdf_file" "$output_file"
    
    # OCR FALLBACK
    if [ ! -s "$output_file" ]; then
        echo "OCR REQUIRED FOR: $pdf_file"
        convert -density 300 "$pdf_file" -depth 8 "temp_${base_name}.tiff"
        tesseract "temp_${base_name}.tiff" "./00_GRIND_OUTPUT/SRC_${base_name}" -l nld
        rm "temp_${base_name}.tiff"
    fi
done
echo "[V] GRIND COMPLETE."

```

**OPERATIE KLAAR VOOR EXECUTION. SUCCES.**
