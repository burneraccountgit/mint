Om de kernel panic mechanisch te bewijzen en de conflicterende OPSEC-instellingen te valideren, is hier het script voor de **Forensische Audit & Validatie**.

Dit script is modulair opgebouwd: het voert eerst de noodzakelijke ontsluiting uit en start daarna de diepe inspectie van de boot-chain en hardening-parameters zonder wijzigingen aan te brengen.

```bash
# =================================================================
# SCRIPT: FORENSISCHE AUDIT & OPSEC VALIDATIE (LIVEBOOT)
# Doel: Mechanisch bewijs leveren voor Kernel Panic (unknown-block 0,0)
# =================================================================

# 1. OMGEVING PREPAREREN (UNLOCK & MOUNT)
sudo cryptsetup open /dev/sda3 cryptdata
sudo vgchange -ay
sudo mount /dev/mapper/vgmint-root /mnt
sudo mount /dev/sda2 /mnt/boot
sudo mount /dev/sda1 /mnt/boot/efi

# 2. VALIDATIE-LOG INITIALISEREN
LOG="/media/mint/USB-STAAFJE/MINT_BACKUP/audit_report_$(date +%Y%m%d_%H%M%S).txt"
{
  echo "=== BOOT CHAIN VALIDATIE ==="
  echo "[1] UUID Check sda3:"
  blkid /dev/sda3
  
  echo -e "\n[2] Crypttab Inhoud:"
  cat /mnt/etc/crypttab
  
  echo -e "\n[3] Grub Configuration (Kernel Parameters):"
  grep "GRUB_CMDLINE_LINUX" /mnt/etc/default/grub
  
  echo -e "\n=== OPSEC & HARDENING CONFLICT ANALYSIS ==="
  echo "[4] Sysctl Lockdown Check:"
  grep -r "kernel.modules_disabled" /mnt/etc/sysctl.conf /mnt/etc/sysctl.d/
  
  echo -e "\n[5] Boot Partition Overhead Check:"
  df -h /mnt/boot
  
  echo -e "\n[6] AppArmor Profile Status:"
  ls -l /mnt/etc/apparmor.d/ | head -n 20

  echo -e "\n=== INITRAMFS INTEGRITY INSPECTION ==="
  echo "[7] Initrd Bestand Groottes (Detecteren 0-byte/corruptie):"
  ls -lh /mnt/boot/initrd.img*
  
} | tee "$LOG"

# 3. CHROOT VOOR DIEPE INSPECTIE (OPTIONEEL)
echo -e "\n--- Audit voltooid. Rapport opgeslagen in: $LOG ---"
echo "Wil je chroot binnengaan voor verdere handmatige validatie? [y/N]"
read -r answer
if [ "$answer" != "${answer#[Yy]}" ]; then
    # Bind mounts voor chroot
    for i in /dev /dev/pts /proc /sys /run; do sudo mount -B $i /mnt$i; done
    sudo chroot /mnt
fi

```

### Waarom deze stappen noodzakelijk zijn voor jouw validatie:

* **UUID vs Crypttab:** De fout `unknown-block(0,0)` ontstaat vaak als de UUID in de bootloader niet exact matcht met de UUID in de ontsleutelde `/etc/crypttab`.
* **Kernel Module Lockdown:** Als `kernel.modules_disabled = 1` aanwezig is in je sysctl-instellingen, wordt gecontroleerd of deze te vroeg wordt aangeroepen, wat het laden van de LUKS-drivers blokkeert.
* **Initrd Inspectie:** De bestandsgrootte-check (Stap 7) valideert of de `initramfs` correct is opgebouwd (tientallen MB's) of dat een eerdere crash een corrupt 0-byte bestand heeft achtergelaten.
* **Grub Parameters:** Er wordt gezocht naar de `root=/dev/mapper/...` parameter om te bevestigen dat de kernel naar de juiste plek kijkt na ontsleuteling.

**Instructie:** Sla de code hierboven op als `audit.sh` op je bureaublad in de Liveboot, maak het uitvoerbaar met `chmod +x audit.sh` en draai het met `./audit.sh`. Kopieer de output van het rapport hiernaartoe voor de finale conclusie over de schuldige OPSEC-regel.
