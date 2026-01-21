**SITREP: OPERATIONAL MISUNDERSTANDING DETECTED**

**GEEN ZORGEN, OPERATOR.** Je haalt twee concepten door elkaar. Laten we dit ontzenuwen met pure logica.

### DE ANALYSE: SWAP vs. OVERCLOCKING

1. **Overclocking (Gevaarlijk):** Dit is het verhogen van de *snelheid* (Voltage/Herz) van je CPU/GPU. Dit creëert hitte en kan je hardware **fysiek slopen**.
2. **Swap File (Veilig):** Dit is puur **opslagruimte** op je harde schijf die wordt gebruikt als "nood-RAM" geheugen.
* *Analogie:* Je RAM is je werkbank. Swap is een extra bijzettafel.
* Als je werkbank (16GB RAM) vol ligt met Lean4 formules, schuift Linux spullen naar de bijzettafel (Swap).
* **Het kan je systeem NIET slopen.** Het ergste dat gebeurt als je Swap te groot maakt, is dat je 16GB minder ruimte hebt voor films en games.



### HET ADVIES VOOR JOUW BUILD (16GB RAM)

Jij draait zware taken (Compilers, AI, Lean4).

* **4GB Swap:** Is "standaard" (veilig voor kantoorwerk).
* **16GB Swap:** Is "Combat Ready" (Stelt je in staat om *gigantische* processen te draaien zonder te crashen, én je kunt 'Hibernate' (Slaapstand naar schijf) gebruiken).

**CONCLUSIE:**
Gezien je "Navy Seal" mentaliteit en zware workloads, gaan we voor **MAXIMALE STABILITEIT**. We matchen je RAM. 16GB RAM = 16GB Swap.
Dit kost je 16GB schijfruimte, maar garandeert dat je machine nooit vastloopt door geheugentekort.

---

### **KEYWORD: FINAL_HARDENING_V2 (16GB EDITION)**

*(Dit is het veilige script, aangepast naar jouw specs)*

1. Maak bestand: `nano final_hardening.sh`
2. Verwijder oude tekst (indien aanwezig).
3. Plak onderstaande code.

```bash
#!/bin/bash
# KEYWORD: FINAL_HARDENING_V2
# DOEL: FAIL2BAN & 16GB SWAP (MATCHING RAM VOOR MAX STABILITY)

# CHECK ROOT
if [[ $EUID -ne 0 ]]; then
   echo "CRITICAL: Run as root: sudo $0"
   exit 1
fi

echo "[*] INITIATING FINAL SECURITY & PERFORMANCE LAYER (HEAVY DUTY)..."

# -----------------------------------------------------
# 1. FAIL2BAN DEPLOYMENT (De Digitale Uitsmijter)
# -----------------------------------------------------
echo "[+] INSTALLING FAIL2BAN..."
apt-get install -y fail2ban

# Activeer service
systemctl enable fail2ban
systemctl start fail2ban

if systemctl is-active --quiet fail2ban; then
    echo "[V] FAIL2BAN ACTIVE & MONITORING."
else
    echo "[!] FAIL2BAN FAILED TO START."
fi

# -----------------------------------------------------
# 2. SWAP EXPANSION (16GB - RAM MATCH)
# -----------------------------------------------------
# Omdat je zware wiskundige berekeningen doet, willen we niet crashen.
# We reserveren 16GB op de schijf als veiligheidsbuffer.
SWAP_FILE="/swapfile_extended"
SWAP_SIZE="16G"

# Check of we genoeg ruimte hebben (simpele check)
FREE_SPACE=$(df -BG / | awk 'NR==2 {print $4}' | sed 's/G//')
if [[ "$FREE_SPACE" -lt 20 ]]; then
    echo "[!] WAARSCHUWING: Minder dan 20GB vrije ruimte. 16GB Swap is riskant."
    echo "    Aborting Swap creation. Fail2Ban is wel geïnstalleerd."
    exit 1
fi

if [ -f "$SWAP_FILE" ]; then
    echo "[!] INFO: $SWAP_FILE bestaat al. Geen actie nodig."
else
    echo "[+] GENERATING $SWAP_SIZE SWAPFILE (DIT DUURT EVEN)..."
    
    # Maak de file
    fallocate -l $SWAP_SIZE $SWAP_FILE
    
    # Beveilig de rechten (alleen root mag lezen)
    chmod 600 $SWAP_FILE
    
    # Formatteer als swap
    mkswap $SWAP_FILE
    
    # Activeer direct
    swapon $SWAP_FILE
    
    # Maak permanent
    if ! grep -q "$SWAP_FILE" /etc/fstab; then
        echo "$SWAP_FILE none swap sw 0 0" >> /etc/fstab
        echo "[V] SWAP ADDED TO FSTAB (PERSISTENT)."
    fi
    
    echo "[V] SWAP CAPACITY INCREASED TO +16GB."
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

### UITVOEREN

```bash
chmod +x final_hardening.sh
sudo ./final_hardening.sh

```

**DIT IS VEILIG. JE SYSTEEM BLIJFT KOEL, MAAR KAN NU ELKE BELASTING AAN.**
