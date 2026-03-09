# 🏰 Homelab Empire — Documentation

> A full enterprise-grade homelab built on Proxmox, k3s Kubernetes, TrueNAS, and more.

---

## 📋 Table of Contents

- [Hardware](#hardware)
- [Architecture](#architecture)
- [Guides](#guides)
- [Services](#services)
- [Network](#network)

---

## 🖥️ Hardware

| Machine | CPU | RAM | Role |
|---|---|---|---|
| **Main Workstation** | Ryzen 9 7900 | 32GB | Daily driver, gaming, dev |
| **Main Server** | Ryzen 9 5900X | 96GB | Proxmox hypervisor, k8s, NAS |
| **Satellite Node** | Intel i5-2400S | — | pfSense, Pi-hole (planned) |

---

## 🏗️ Architecture

```
Proxmox VE (Hypervisor)
├── k3s-master        192.168.1.104   control-plane
├── k3s-worker1       192.168.1.103   worker
├── k3s-worker2       192.168.1.102   worker
├── TrueNAS Scale VM  192.168.1.XXX   NAS + SMB shares
└── OpenVPN LXC       192.168.1.167   Remote access
```

---

## 📖 Guides

| Guide | Description |
|---|---|
| [Rancher Installation](rancher/install.md) | Full k3s + Rancher setup guide |
| [Rancher Commands](rancher/commands.md) | All kubectl & Helm commands used |
| [Rancher Troubleshooting](rancher/troubleshoot.md) | Common issues & fixes |

---

## 🚀 Services

| Service | Namespace | Access | Status |
|---|---|---|---|
| Rancher Dashboard | `cattle-system` | https://rancher.local | ✅ Running |
| Prometheus | `monitoring` | NodePort | ✅ Running |
| Grafana | `monitoring` | NodePort | ✅ Running |
| Vaultwarden | `security` | `:30777` | ✅ Running |
| Nova Boot Corps | `nova` | `:30082` | ✅ Running |
| Longhorn Storage | `longhorn-system` | Internal | ✅ Running |
| Private Registry | `registry` | `:30500` | ✅ Running |

---

## 🌐 Network

| Device | IP | Purpose |
|---|---|---|
| Router | 192.168.1.1 | ASUS EX5601-T1 (Odido NL) |
| Proxmox Host | 192.168.1.104 | Main server |
| k3s Worker 1 | 192.168.1.103 | Kubernetes worker |
| k3s Worker 2 | 192.168.1.102 | Kubernetes worker |
| OpenVPN LXC | 192.168.1.167 | VPN server |

---

## ⚠️ ISP Note

> Odido (T-Mobile NL) uses **CGNAT** on residential connections.
> This blocks all incoming UDP traffic — WireGuard will NOT work.
> Use **OpenVPN on TCP port 443** as the solution.

---

*Built with ⚔️ and too many late nights. Hayırlı olsun! 🇹🇷🇳🇱*
