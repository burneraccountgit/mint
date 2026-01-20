Het openen van de encryptie en LVM is gelukt ("2 logical volume(s)... now active"). Echter, de `for`-loop om de systeem mappen te koppelen faalt door een conflict met `sudo`. Hierdoor is je `chroot` omgeving nog **niet** compleet.

We doen dit handmatig, regel voor regel, om de `pty` error te omzeilen.

### Correctie Module 1b: Handmatige Binds

Voer deze regels stuk voor stuk uit. Als er geen output verschijnt, is het gelukt.

```bash
sudo mount --bind /dev /mnt/dev
sudo mount --bind /dev/pts /mnt/dev/pts
sudo mount --bind /proc /mnt/proc
sudo mount --bind /sys /mnt/sys
sudo mount --bind /run /mnt/run
```

```
mint@mint:~$ sudo mount --bind /dev /mnt/dev
sudo mount --bind /dev/pts /mnt/dev/pts
sudo mount --bind /proc /mnt/proc
sudo mount --bind /sys /mnt/sys
sudo mount --bind /run /mnt/run
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
sudo: unable to allocate pty: No such device
mint@mint:~$ 
```

### Module 2: Chroot Starten

Nu alles vastgeknoopt is, kunnen we de omgeving binnengaan.

```bash
sudo chroot /mnt

```

> **Check:** Als dit lukt, verandert je prompt (bijvoorbeeld naar `root@mint` of `#`).

Zodra je "binnen" bent, voer direct dit commando uit om te zien of we internet en schijfruimte hebben voor de reparatie:

```bash
# Check ruimte op /boot (Mag niet 100% zijn)
df -h /boot

```

Laat even weten wat de output van `df -h /boot` is.
