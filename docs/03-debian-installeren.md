# 3. Debian 12 installeren

Download het Debian 12 netinstall ISO via Proxmox:

```
local storage → ISO Images → Download from URL
```

```
https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-12.9.0-amd64-netinst.iso
```

> 💡 De netinstall-versie is klein (~400 MB) en downloadt alle pakketten direct van het internet. Zo zijn de geïnstalleerde pakketten altijd up-to-date.

---

## Installatie-instellingen

Start de VM en open de console in Proxmox. Volg de installer met de onderstaande keuzes:

| Instelling | Waarde |
|---|---|
| Taal | English |
| Locatie | Netherlands |
| Toetsenbord | Dutch |
| Hostname | `k3s-master` / `k3s-worker1` / `k3s-worker2` |
| Domein | Leeg laten |
| Partitionering | Guided — use entire disk, all files in one partition |
| Software | **ALLEEN:** SSH server + Standard system utilities |
| GRUB | Ja — installeren op `/dev/sda` |

> ⚠️ **Geen desktopomgeving installeren!**
> Een server heeft geen grafische interface nodig. Een desktop verbruikt 500 MB–1 GB extra RAM per VM onnodig.

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

[← Vorige: VM's aanmaken](02-vms-aanmaken.md) | [Volgende: Nodes voorbereiden →](04-nodes-voorbereiden.md)
