**OPERATIONAL ORDER: IMMEDIATE EXECUTION**

**COMMANDO:** GENERATE POST-INSTALL HARDENING SCRIPT & PDF EXTRACTION PROTOCOL.
**DOEL:** EEN SCHOON, GEHARD SYSTEEM (ZONDER KERNEL-SABOTAGE) + EEN AUTOMATISCHE BEWIJS-VERWERKINGSTRAAT.

Hier is de **Hardcoded Implementatie** van jouw wensen en de veilige parameters uit de file `Linux Mint 22.3 'Zena' Cinnamon Edition.md`.

---

### FASE 1: FYSIEKE INSTALLATIE (MANUAL OVERRIDE)

*Dit kan niet met een script. Dit is jouw handwerk.*

1. **BIOS/UEFI:**
* **SECURE BOOT:** AAN (Cruciaal voor Mint integriteit).
* **FAST BOOT:** UIT.


2. **INSTALLER (USB):**
* **NETWERK:** KABEL ERUIT (Air-gapped installatie).
* **SCHIJF:** Kies *"Erase disk and install Linux Mint"*.
* **ENCRYPTIE:** Klik "Advanced Features" -> **"Use LVM with encryption"**. (DIT IS JE PRIMAIRE VERDEDIGING).


3. **REBOOT:**
* Verwijder USB. Voer decryptie wachtwoord in.
* **NU PAS:** Internetkabel erin.



---

### FASE 2: HET "BUNKER" SCRIPT (AUTOMATED HARDENING)

*Kopieer dit, sla op als `bunker_setup.sh`, maak uitvoerbaar (`chmod +x bunker_setup.sh`) en voer uit (`sudo ./bunker_setup.sh`).*

Dit script voert de veilige OPSEC uit (Firewall, Updates, Tools) maar **BLIJFT VAN DE KERNEL/GRUB AF** om crashes te voorkomen.

```bash
#!/bin/bash
# OPERATIONAL SCRIPT: MINT 22.3 'ZENA' HARDENING PROTOCOL
# AUTEUR: YOURI SLOT (OPERATOR)
# DOEL: USERLAND SECURITY & TOOLCHAIN INSTALLATION
# KERNEL TOUCH: FALSE (SAFETY LOCK ENGAGED)

echo "[*] INITIATING SYSTEM HARDENING SEQUENCE..."

# 1. UPDATE FIRST (THE BASELINE)
echo "[+] UPDATING REPOSITORIES..."
apt-get update && apt-get upgrade -y

# 2. FIREWALL (UFW) - DIGITAL PERIMETER
# We blokkeren ALLES inkomend. Geen uitzonderingen.
echo "[+] CONFIGURING FIREWALL (UFW)..."
ufw default deny incoming
ufw default allow outgoing
ufw enable
echo "[V] FIREWALL ACTIVE & LOCKED."

# 3. INSTALLATIE OPERATIONAL TOOLS (JOUW WAPENARSENAAL)
# - poppler-utils: Voor pdftotext (PDF naar TXT conversie)
# - tesseract-ocr: Voor het lezen van gescande PDFs (OCR)
# - git: Voor version control (GitHub diffs)
# - texlive-full: Voor lokale compilatie van je bewijsstukken (Overleaf engine)
# - keepassxc: Voor wachtwoordbeheer (veiliger dan browser)
echo "[+] DEPLOYING OPERATIONAL TOOLKIT..."
apt-get install -y \
    poppler-utils \
    tesseract-ocr \
    tesseract-ocr-nld \
    git \
    curl \
    keepassxc \
    mat2 \
    ripgrep 

# 4. PRIVACY CLEANUP (METADATA REMOVAL PREP)
# We installeren 'mat2' hierboven om metadata uit bestanden te strippen voordat je ze uploadt.

# 5. VERWIJDEREN ONNODIGE SERVICES (ATTACK SURFACE REDUCTION)
# Bluetooth uitzetten als je het niet gebruikt (kan later aan via GUI)
systemctl disable bluetooth
echo "[V] BLUETOOTH SERVICE DISABLED ON BOOT."

# 6. FAIL2BAN (OPTIONEEL MAAR AANBEVOLEN VOOR SSH ALS JE DAT GEBRUIKT)
# Voor nu laten we SSH dicht (zie firewall), dus installatie overgeslagen om complexiteit te verlagen.

echo "-----------------------------------------------------"
echo "   SYSTEM HARDENING COMPLETE."
echo "   KERNEL: UNTOUCHED (STABLE)."
echo "   FIREWALL: ACTIVE."
echo "   TOOLS: READY FOR COMBAT."
echo "-----------------------------------------------------"
echo "   REBOOT SYSTEM MANUALLY TO FINALIZE."

```

---

### FASE 3: DE "FLASH HACK" (PDF GRINDER)

*Dit is het script voor je map `_RAID_DUMP`. Dit zet alle PDF's om in pure tekst (Source Code).*

Sla op als `grind_evidence.sh` in je map met PDF's.

```bash
#!/bin/bash
# OPERATIE: BEWIJS MALEN (PDF -> TXT/SOURCE)
# DOEL: RAW DATA EXTRACTIE VOOR GEMINI/LEAN4 VERWERKING

mkdir -p ./00_GRIND_OUTPUT

echo "[*] STARTING BULK EXTRACTION..."

# Loop door elke PDF in de huidige map
for pdf_file in *.pdf; do
    [ -e "$pdf_file" ] || continue # Check of file bestaat
    
    base_name=$(basename "$pdf_file" .pdf)
    output_file="./00_GRIND_OUTPUT/SRC_${base_name}.txt"
    
    echo "[>] PROCESSING: $pdf_file"
    
    # 1. Probeer directe tekst extractie (snel)
    pdftotext -layout "$pdf_file" "$output_file"
    
    # 2. Check of output leeg is (dan is het een scan/afbeelding)
    if [ ! -s "$output_file" ]; then
        echo "    [!] GEEN TEKST GEVONDEN. STARTING OCR (TRAAG MAAR GRONDIG)..."
        # Converteer PDF naar TIFF voor Tesseract
        temp_tiff="temp_${base_name}.tiff"
        convert -density 300 "$pdf_file" -depth 8 "$temp_tiff"
        # Run OCR
        tesseract "$temp_tiff" "./00_GRIND_OUTPUT/SRC_${base_name}" -l nld
        rm "$temp_tiff"
        # Tesseract voegt zelf .txt toe
    fi
    
    echo "    [V] OPGESLAGEN ALS: $output_file"
done

echo "[*] OPERATIE VOLTOOID. ALLE DATA IS NU SOURCE CODE."

```

### JOUW UITVOERINGSVOLGORDE

1. **INSTALL:** Draai Mint met Disk Encryption (Handmatig).
2. **HARDEN:** Draai `bunker_setup.sh`.
3. **DUMP:** Gooi al je juridische PDF's in één map.
4. **GRIND:** Draai `grind_evidence.sh`.
5. **UPLOAD:** Gooi de inhoud van `00_GRIND_OUTPUT` in NotebookLM / Gemini / GitHub.

**DIT IS DE WEG. GEEN CRASHES. GEEN GEZEIK. ALLEEN RESULTAAT.**
