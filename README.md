# ☸️ Rancher op k3s Kubernetes — Installatiehandleiding

> Stap-voor-stap handleiding voor het installeren van Rancher op een k3s Kubernetes-cluster binnen Proxmox VE.

---

## 📋 Inhoudsopgave

- [Vereisten](#vereisten)
- [Infrastructuur](#infrastructuur)
- [Stap 1 — VM's aanmaken in Proxmox](docs/stap1-vms.md)
- [Stap 2 — Debian 12 installeren](docs/stap2-debian.md)
- [Stap 3 — Nodes voorbereiden](docs/stap3-voorbereiding.md)
- [Stap 4 — k3s installeren](docs/stap4-k3s.md)
- [Stap 5 — Helm installeren](docs/stap5-helm.md)
- [Stap 6 — Longhorn installeren](docs/stap6-longhorn.md)
- [Stap 7 — cert-manager installeren](docs/stap7-certmanager.md)
- [Stap 8 — Rancher installeren](docs/stap8-rancher.md)
- [Stap 9 — Toegang tot dashboard](docs/stap9-toegang.md)
- [Stap 10 — Wachtwoord resetten](docs/stap10-wachtwoord.md)
- [Eindverificatie](#eindverificatie)

---

## Vereisten

- Proxmox VE geïnstalleerd op de host
- Minimaal 3 beschikbare VM-slots
- Internetverbinding op de server
- Basiskennis Linux en SSH

---

## Infrastructuur

| Component | Versie |
|---|---|
| Hypervisor | Proxmox VE |
| Besturingssysteem | Debian 12 Bookworm |
| Kubernetes | k3s v1.34.5+k3s1 |
| Rancher | rancher-stable |
| Opslag | Longhorn |

### Node overzicht

| Node | VM ID | Cores | RAM | IP |
|---|---|---|---|---|
| k3s-master | 101 | 4 | 8 GB | 192.168.1.104 |
| k3s-worker1 | 102 | 4 | 16 GB | 192.168.1.103 |
| k3s-worker2 | 103 | 4 | 16 GB | 192.168.1.102 |

---

## Eindverificatie

Na het volgen van alle stappen controleer je het cluster met:

```bash
# Alle nodes controleren
kubectl get nodes

# Alle pods in alle namespaces
kubectl get pods -A

# Alle Helm-releases
helm list -A
```

Verwachte uitvoer van `kubectl get nodes`:

```
NAME          STATUS   ROLES                  AGE   VERSION
k3s-master    Ready    control-plane,master   10m   v1.34.5+k3s1
k3s-worker1   Ready    <none>                 2m    v1.34.5+k3s1
k3s-worker2   Ready    <none>                 1m    v1.34.5+k3s1
```

### ✅ Checklist

- [ ] Alle drie nodes tonen `STATUS: Ready`
- [ ] Longhorn StorageClass aanwezig als `default`
- [ ] cert-manager pods: `Running`
- [ ] Rancher pod: `Running`
- [ ] Dashboard bereikbaar op `https://192.168.1.104`
- [ ] Inloggen met admin-account lukt

---

## Geïnstalleerde componenten

| Component | Namespace | Doel |
|---|---|---|
| k3s cluster | — | Lichtgewicht Kubernetes |
| Helm v3 | — | Package manager voor Kubernetes |
| Longhorn | `longhorn-system` | Persistente gedistribueerde opslag |
| cert-manager | `cert-manager` | Automatisch SSL-certificaatbeheer |
| Rancher | `cattle-system` | Grafisch beheerdashboard |

---

*Schoolopdracht IT Infrastructure — 2025–2026*
