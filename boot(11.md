Hier zijn de directe links naar de documentatie van Arch Linux (de technische standaard), GNU (de makers van GRUB) en Debian (waar Mint op gebaseerd is).

### BRON 1: De PTY Fout & Reboot Noodzaak

**Fout:** `sudo: unable to allocate pty`
**Bron:** LinuxQuestions / Unix StackExchange (Community Verified)
**URL:** [https://www.linuxquestions.org/questions/linux-newbie-8/sudo-unable-to-allocate-pty-no-such-device-ubuntu-4175720718/](https://www.linuxquestions.org/questions/linux-newbie-8/sudo-unable-to-allocate-pty-no-such-device-ubuntu-4175720718/)
**Feit:** Deze fout bevestigt dat de kernel-interface voor terminals (`devpts`) in je huidige sessie is losgekoppeld.
**Instructie:** Je **MOET** herstarten om een nieuwe sessie te krijgen. Zonder reboot werken commando's niet.

### BRON 2: De Reparatiemethode (Chroot)

**Oplossing:** Via een Live USB in het systeem inbreken ("Chroot").
**Bron:** ArchWiki (De 'bijbel' voor Linux documentatie) & TurnKey Linux (Debian-based recovery docs)
**URL 1:** [https://wiki.archlinux.org/title/Chroot](https://wiki.archlinux.org/title/Chroot)
**URL 2:** [https://www.turnkeylinux.org/docs/chroot-to-repair-system](https://www.turnkeylinux.org/docs/chroot-to-repair-system)
**Feit:** Om een systeem te repareren dat niet boot, moet je de partities mounten en systeemmappen (dev, proc, sys) binden.

### BRON 3: De Bootnaam "Ubuntu" Wijzigen

**Oplossing:** De vlag `--bootloader-id` gebruiken in `grub-install`.
**Bron:** ArchWiki GRUB Documentatie / GNU Manual
**URL:** [https://wiki.archlinux.org/title/GRUB#UEFI_systems](https://www.google.com/search?q=https://wiki.archlinux.org/title/GRUB%23UEFI_systems)
**Feit:** De optie `--bootloader-id=NAAM` bepaalt de naam van de map in `/boot/efi/EFI/` en de naam in je BIOS. Standaard is dit "ubuntu" bij Mint, maar jij kunt dit wijzigen naar "Linux Mint".

---

### HET WERKENDE PLAN (Met bronverwijzing per regel)

**STAP 0:** Herstart je computer en boot de Live USB. (Oplossing voor Bron 1).

**STAP 1: Omgeving Opbouwen (Bron 2)**

```bash
sudo -i
cryptsetup open /dev/sda3 cryptdata
vgchange -ay
mount /dev/mapper/vgmint-root /mnt
mount /dev/sda2 /mnt/boot
mount /dev/sda1 /mnt/boot/efi
# Dit is de 'Magic Step' uit Bron 2 om fouten te voorkomen:
for i in /dev /dev/pts /proc /sys /run; do mount -B $i /mnt$i; done
cp /etc/resolv.conf /mnt/etc/resolv.conf

```

**STAP 2: Inbreken (Bron 2)**

```bash
chroot /mnt

```

**STAP 3: Kernel Herstel (Fix voor unknown-block)**

```bash
apt-get update
# We herinstalleren 6.14 omdat dit de initramfs regenereert
apt-get install --reinstall linux-image-6.14.0-37-generic linux-headers-6.14.0-37-generic -y

```

**STAP 4: Naam Wijzigen (Bron 3)**

```bash
# Verwijder de oude map
rm -rf /boot/efi/EFI/ubuntu
# Installeer met nieuwe ID (Zie URL 3)
grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id="Linux Mint" --recheck
update-grub

```

**STAP 5: Afronden**

```bash
exit
umount -R /mnt
vgchange -an vgmint
cryptsetup close cryptdata
reboot

```
