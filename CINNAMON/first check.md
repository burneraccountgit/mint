**SITREP: KRITIEKE WAARSCHUWING - OPSLAG VOL**

**STATUS:** **STOP DIRECT MET INSTALLEREN.**
Je analyse is correct, maar je conclusie ("fuck it, nog een keer proberen") gaat falen.

De error:

> *"installed initramfs-tools package post-installation script subprocess returned error exit status 1"*

In combinatie met je waarschuwing:

> *"boot warning niet veel ruimte over in boot"*

**DIAGNOSE:**
Je `/boot` partitie zit **VOL**.
Elke keer als je een driver (Nvidia) installeert of update, moet Linux een nieuwe `initramfs` (startbestand) genereren. Dit bestand is groot (80MB+).
Als `/boot` vol is, faalt het schrijven halverwege  Script crasht met `exit status 1`  Installatie breekt af.

Als je nu de 535 driver probeert te installeren, zal die **OOK FALEN** omdat hij diezelfde ruimte nodig heeft. Je duwt een kurk in een volle fles.

---

### **PROTOCOL: RUIMTE MAKEN (BOOT CLEANUP)**

Voer deze stappen uit **VOORDAT** je Driver Manager weer aanraakt.

**STAP 1: CHECK DE RUIMTE**
Open terminal en typ:

```bash
df -h /boot

```

*Als 'Use%' op 95% of 100% staat, is dit bevestigd.*

**STAP 2: DE AUTOMATISCHE SCHOONMAAK (PROBEER DIT EERST)**
Dit commando verwijdert automatisch oude kernels die je niet meer gebruikt.

```bash
sudo apt-get autoremove --purge

```

*Als dit lukt zonder errors: **HERSTARTEN** en dan pas Nvidia 535 proberen.*

---

**STAP 3: DE HANDMATIGE SCHOONMAAK (ALS STAP 2 FAALT)**
Als `apt` klaagt dat het "broken" is en niks wil doen, moeten we handmatig ruimte maken.

1. **Kijk welke kernel je NU gebruikt (deze MAG JE NIET VERWIJDEREN):**
```bash
uname -r

```


*(Schrijf dit nummer op, bijv. `6.8.0-52-generic`)*
2. **Kijk welke kernels er allemaal zijn:**
```bash
dpkg --list | grep linux-image

```


3. **Verwijder een OUDE versie (NIET degene uit punt 1):**
Stel je draait op `6.8.0-52`. En je ziet ook `6.5.0-10` of `5.15.0-90` in de lijst staan.
Verwijder dan die oude:
```bash
sudo apt-get purge linux-image-OudeVersieNummer-generic linux-headers-OudeVersieNummer-generic

```


*(Vervang `OudeVersieNummer` door het nummer dat je in de lijst zag staan).*

**EINDSTAAT:**
Pas als `/boot` weer ruimte heeft (check met `df -h /boot`), zal de Nvidia installatie (die `update-initramfs` triggert) slagen.

**VOER UIT.**
