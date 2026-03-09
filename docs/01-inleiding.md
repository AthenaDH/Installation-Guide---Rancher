# 1. Inleiding

In deze handleiding wordt stap voor stap uitgelegd hoe je Rancher installeert op een k3s Kubernetes-cluster dat draait op virtuele machines binnen Proxmox VE.

**Rancher** is een open-source platform voor het beheren van Kubernetes-clusters via een grafische webinterface. Het biedt een overzichtelijk dashboard waarmee je applicaties kunt deployen, resources kunt monitoren en clusters kunt beheren — zonder dat je elk commando handmatig via de terminal moet uitvoeren.

**k3s** is een lichtgewicht versie van Kubernetes, ontwikkeld door Rancher Labs. Het heeft dezelfde API en commando's als volledige Kubernetes, maar met minder overhead — ideaal voor een homelab of schoolomgeving.

---

## Wat wordt er geïnstalleerd?

| Component | Doel |
|---|---|
| Proxmox VE | Hypervisor voor het draaien van VM's |
| Debian 12 Bookworm | Besturingssysteem op elke VM |
| k3s | Lichtgewicht Kubernetes-cluster (1 master + 2 workers) |
| Helm v3 | Package manager voor Kubernetes |
| Longhorn | Gedistribueerde opslag voor persistente data |
| cert-manager | Automatisch SSL-certificaatbeheer (vereist door Rancher) |
| Rancher | Grafisch beheerdashboard voor het cluster |

---

## Vereiste kennis

- Basiskennis Linux (bestanden bewerken, services starten)
- Basiskennis netwerken (IP-adressen, poorten)
- Bekend zijn met SSH

---

## Gebruikte infrastructuur

| Instelling | Waarde |
|---|---|
| Hypervisor | Proxmox VE |
| Master node IP | 192.168.1.104 |
| Worker 1 IP | 192.168.1.103 |
| Worker 2 IP | 192.168.1.102 |
| OS per VM | Debian 12 Bookworm (netinst) |
| k3s versie | v1.34.5+k3s1 |
| Rancher kanaal | rancher-stable |

---

[Volgende stap: VM's aanmaken →](02-vms-aanmaken.md)
