**SITREP: LAATSTE VERDEDIGINGSLINIE & PRESTATIE-BOOST**

**BEVESTIGD.** We installeren **Fail2Ban** (actieve indringer-blokkade) en we **vergroten je Swap-geheugen** (virtueel RAM) met 4GB. Omdat je Full Disk Encryption gebruikt (LVM+LUKS), is deze nieuwe swapfile automatisch ook versleuteld. Veilig dus.

Hier is het script.

---

### **KEYWORD: FINAL_HARDENING**

*(Opslaan als `final_hardening.sh`)*

```bash
#!/bin/bash
# KEYWORD: FINAL_HARDENING
# DOEL: FAIL2BAN INSTALLATIE & SWAP UITBREIDING (4GB EXTRA)

# CHECK ROOT
if [[ $EUID -ne 0 ]]; then
   echo "CRITICAL: Run as root: sudo $0"
   exit 1
fi

echo "[*] INITIATING FINAL SECURITY & PERFORMANCE LAYER..."

# -----------------------------------------------------
# 1. FAIL2BAN DEPLOYMENT (De Digitale Uitsmijter)
# -----------------------------------------------------
echo "[+] INSTALLING FAIL2BAN..."
apt-get install -y fail2ban

# Activeer service
systemctl enable fail2ban
systemctl start fail2ban

# Bevestig status
if systemctl is-active --quiet fail2ban; then
    echo "[V] FAIL2BAN ACTIVE & MONITORING."
else
    echo "[!] FAIL2BAN FAILED TO START."
fi

# -----------------------------------------------------
# 2. SWAP EXPANSION (Geheugenbuffer vergroten)
# -----------------------------------------------------
# We maken een extra swapfile van 4GB.
# Omdat je disk encrypted is, is deze file dat ook.
SWAP_FILE="/swapfile_extended"
SWAP_SIZE="4G"

if [ -f "$SWAP_FILE" ]; then
    echo "[!] INFO: $SWAP_FILE bestaat al. Geen actie nodig."
else
    echo "[+] GENERATING $SWAP_SIZE SWAPFILE..."
    
    # Maak de file (snel)
    fallocate -l $SWAP_SIZE $SWAP_FILE
    
    # Beveilig de rechten (alleen root mag lezen)
    chmod 600 $SWAP_FILE
    
    # Formatteer als swap
    mkswap $SWAP_FILE
    
    # Activeer direct
    swapon $SWAP_FILE
    
    # Maak permanent (zodat het na reboot blijft werken)
    if ! grep -q "$SWAP_FILE" /etc/fstab; then
        echo "$SWAP_FILE none swap sw 0 0" >> /etc/fstab
        echo "[V] SWAP ADDED TO FSTAB (PERSISTENT)."
    fi
    
    echo "[V] SWAP CAPACITY INCREASED."
fi

# -----------------------------------------------------
# 3. SITUATION REPORT
# -----------------------------------------------------
echo "-----------------------------------------------------"
echo "   FINAL STATUS CHECK:"
echo "   FAIL2BAN:"
systemctl status fail2ban | grep "Active:"
echo ""
echo "   MEMORY (SWAP):"
free -h | grep "Swap:"
echo "-----------------------------------------------------"
echo "   SYSTEM OPTIMIZED."

```

### UITVOEREN (HETZELFDE PROTOCOL)

1. Maak bestand: `nano final_hardening.sh` (Plakken, Opslaan `Ctrl+O`, Sluiten `Ctrl+X`).
2. Maak uitvoerbaar: `chmod +x final_hardening.sh`
3. Voer uit: `sudo ./final_hardening.sh`

**HIERMEE IS JE SYSTEEM GEHARD, GEUPDATE EN OPTIMALISEERD VOOR ZWAAR REKENWERK (SWAP).**
