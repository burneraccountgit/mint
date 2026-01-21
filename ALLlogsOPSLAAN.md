sudo tar -cvpzf /pad/naar/backup.tar.gz /mnt/etc | tee /media/mint/USB-STAAFJE/MINT_BACKUP/backup.log

---

Gebruik de "GDB" methode (De tekst uit het geheugen trekken)
Dit is een geavanceerde truc om de tekst direct uit het lopende proces van je terminal te stelen.

    Open een tweede terminalvenster.
    Installeer een kleine tool (dit duurt 2 seconden in liveboot):
    sudo apt update && sudo apt install gdb -y
    Vind het proces-ID (PID) van je vastgelopen terminal:
    pgrep -l terminal (meestal gnome-terminal of xfce4-terminal).
    Gebruik dit commando om de buffer van die terminal te dumpen naar je SSD:
    sudo gcore <PID_VAN_STAP_3>

Dit maakt een groot bestand (core.<PID>). Daar zit alle tekst in. Je kunt de leesbare tekst er daarna uitvissen met:
strings core.<PID> > /media/mint/USB-STAAFJE/MINT_BACKUP/terminal_dump.txt

---

