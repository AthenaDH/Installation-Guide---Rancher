# Stap 1 — VM's aanmaken in Proxmox

[← Terug naar README](../README.md) | [Stap 2 →](stap2-debian.md)

---

## Uitleg

Voor het cluster zijn drie Debian 12 VM's nodig: één master-node en twee worker-nodes. De master beheert het cluster; de workers draaien de daadwerkelijke applicaties.

---

## VM-instellingen

Klik in Proxmox rechtsboven op **Create VM** en gebruik de onderstaande instellingen voor elke VM.

| Instelling | Waarde | Waarom |
|---|---|---|
| Machine type | `q35` | Ondersteunt moderne UEFI en PCIe-apparaten |
| BIOS | `OVMF (UEFI)` | Vereist voor Debian 12 |
| SCSI Controller | `VirtIO SCSI Single` | Beste schijfprestaties via paravirtualisatie |
| Netwerkmodel | `VirtIO` | Snelste virtuele netwerkkaart |
| Schijfcache | `Write Back` | Verbeterde schrijfprestaties |
| Discard | `Aan` | Geeft vrijgekomen ruimte terug aan de host |
| SSD Emulation | `Aan` | Optimaliseert schijftoegang voor SSD-pools |
| Guest Agent | `Aan` | Communicatie tussen VM en Proxmox-host |

> ⚠️ **Let op:** Schakel TPM **uit** — dit is niet nodig en veroorzaakt problemen.

---

## Resources per node

| Node | VM ID | Cores | RAM | Schijf | IP |
|---|---|---|---|---|---|
| k3s-master | 101 | 4 | 8 GB | 32 GB | 192.168.1.104 |
| k3s-worker1 | 102 | 4 | 16 GB | 64 GB | 192.168.1.103 |
| k3s-worker2 | 103 | 4 | 16 GB | 64 GB | 192.168.1.102 |

---

## Workers klonen (tijdsbesparing)

Na het installeren van de master kun je de VM klonen in plaats van opnieuw installeren:

```
Rechts klikken op k3s-master VM → Clone
  VM ID: 102 | Naam: k3s-worker1 | Mode: Full Clone

Herhaal voor:
  VM ID: 103 | Naam: k3s-worker2 | Mode: Full Clone
```

Verhoog daarna het RAM van beide workers via **Hardware → Memory → 16384 MB**.

---

[← Terug naar README](../README.md) | [Stap 2 →](stap2-debian.md)
