# Stap 2 — Debian 12 installeren

[← Stap 1](stap1-vms.md) | [Stap 3 →](stap3-voorbereiding.md)

---

## ISO downloaden

Download het Debian 12 netinstall ISO via Proxmox:

```
local storage → ISO Images → Download from URL
```

```
https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-12.9.0-amd64-netinst.iso
```

> 💡 De netinstall-versie (~400 MB) downloadt alle pakketten direct van het internet — zo zijn geïnstalleerde pakketten altijd up-to-date.

---

## Installatie-instellingen

Start de VM en open de console in Proxmox. Kies **Install** (niet Graphical install) en gebruik de onderstaande instellingen:

| Keuze | Waarde |
|---|---|
| Taal | English |
| Locatie | Netherlands |
| Toetsenbord | Dutch |
| Hostname | `k3s-master` / `k3s-worker1` / `k3s-worker2` |
| Domein | Leeg laten |
| Root wachtwoord | Sterk wachtwoord — bewaar dit! |
| Partitionering | Guided — use entire disk |
| Partitie-indeling | All files in one partition |
| Software selectie | **Alleen:** SSH server + Standard system utilities |
| GRUB | Ja — installeren op `/dev/sda` |

> ⚠️ **Geen desktopomgeving installeren!** Een server heeft geen grafische interface nodig. Een desktop verbruikt 500 MB–1 GB extra RAM per VM.

---

## Na installatie — inloggen via SSH

Na het herstarten log je in via SSH vanuit je hoofdmachine:

```bash
ssh jouwgebruiker@192.168.1.104
```

Schakel over naar root voor de volgende stappen:

```bash
su -
```

---

[← Stap 1](stap1-vms.md) | [Stap 3 →](stap3-voorbereiding.md)
