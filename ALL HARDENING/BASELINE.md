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
