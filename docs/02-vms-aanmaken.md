# 2. Virtuele machines aanmaken in Proxmox

Voor het cluster zijn drie identieke Debian 12 VM's nodig: één master-node en twee worker-nodes. De master beheert het cluster; de workers draaien de daadwerkelijke applicaties.

---

## VM-instellingen

Maak in Proxmox drie VM's aan via **Create VM** rechtsboven met de onderstaande instellingen:

| Instelling | Waarde | Waarom |
|---|---|---|
| Machine type | `q35` | Modern platform met UEFI en PCIe-ondersteuning |
| BIOS | `OVMF (UEFI)` | Vereist voor Debian 12 |
| SCSI Controller | `VirtIO SCSI Single` | Beste schijfprestaties |
| Netwerkmodel | `VirtIO` | Snelste virtuele netwerkkaart (paravirtualisatie) |
| Schijfcache | `Write Back + Discard + SSD Emulation` | Betere prestaties + TRIM-ondersteuning |
| Guest Agent | `Inschakelen` | Communicatie tussen VM en Proxmox |

---

## Resources per node

| Node | VM ID | Cores | RAM | Schijf | IP |
|---|---|---|---|---|---|
| k3s-master | 101 | 4 | 8 GB | 32 GB | 192.168.1.104 |
| k3s-worker1 | 102 | 4 | 16 GB | 64 GB | 192.168.1.103 |
| k3s-worker2 | 103 | 4 | 16 GB | 64 GB | 192.168.1.102 |

> ⚠️ **Belangrijk:** Workers krijgen meer RAM omdat zij de daadwerkelijke workloads (pods) draaien. De master beheert alleen het cluster.

---

## CPU-type instellen

Stel bij elke VM het CPU-type in op `host` voor maximale prestaties:

```
VM → Hardware → Processors → Type: host
```

Dit geeft de VM directe toegang tot de CPU-instructies van de fysieke host, in plaats van een geëmuleerde processor.

---

[← Vorige: Inleiding](01-inleiding.md) | [Volgende: Debian installeren →](03-debian-installeren.md)
