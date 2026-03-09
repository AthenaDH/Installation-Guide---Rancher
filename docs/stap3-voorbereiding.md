# Stap 3 — Nodes voorbereiden voor Kubernetes

[← Stap 2](stap2-debian.md) | [Stap 4 →](stap4-k3s.md)

---

> ⚠️ Voer alle commando's op deze pagina uit op **elke node** (master én beide workers).

---

## 3.1 APT bronnen bijwerken

```bash
nano /etc/apt/sources.list
```

Vervang de inhoud door:

```
deb http://deb.debian.org/debian bookworm main contrib non-free non-free-firmware
deb http://deb.debian.org/debian bookworm-updates main contrib non-free non-free-firmware
deb http://security.debian.org/debian-security bookworm-security main contrib non-free
```

Daarna:

```bash
apt update && apt upgrade -y
```

---

## 3.2 Benodigde pakketten installeren

```bash
apt install -y curl wget git htop net-tools sudo qemu-guest-agent
systemctl enable qemu-guest-agent
systemctl start qemu-guest-agent
usermod -aG sudo JOUWGEBRUIKERSNAAM
```

| Pakket | Doel |
|---|---|
| `curl` / `wget` | Bestanden downloaden via de terminal |
| `git` | Versiebeheer |
| `htop` | Interactieve procesmonitor |
| `net-tools` | Netwerkdiagnostiek (`ifconfig`, `netstat`) |
| `sudo` | Verhoogde rechten voor gewone gebruiker |
| `qemu-guest-agent` | Communicatie tussen VM en Proxmox-host |

---

## 3.3 Swap uitschakelen

Kubernetes vereist dat swap uitgeschakeld is. Swap kan de scheduler in de war brengen omdat Kubernetes geheugenlimieten strikt beheert en swap die grenzen omzeilt.

```bash
swapoff -a
sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
```

> 💡 De tweede regel zorgt ervoor dat swap ook na een herstart uitgeschakeld blijft door de swap-regel in `/etc/fstab` te commentariëren.

---

## 3.4 Kernelmodules laden

Kubernetes heeft twee kernelmodules nodig voor zijn netwerkfunctionaliteit:

```bash
cat <<EOF >> /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF

modprobe overlay
modprobe br_netfilter
```

| Module | Doel |
|---|---|
| `overlay` | Maakt overlay-filesystems mogelijk — hiermee werken container-images (Docker/containerd stapelt lagen) |
| `br_netfilter` | Laat iptables bridge-verkeer filteren — vereist voor Kubernetes-netwerkcommunicatie tussen pods |

---

## 3.5 Netwerkinstellingen voor Kubernetes

```bash
cat <<EOF >> /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF

sysctl --system
```

| Parameter | Doel |
|---|---|
| `bridge-nf-call-iptables` | Zorgt dat gebridged verkeer door iptables gaat — vereist voor Kubernetes Service networking |
| `ip_forward` | Staat IP-forwarding toe tussen interfaces — zonder dit kunnen pods niet communiceren |

---

[← Stap 2](stap2-debian.md) | [Stap 4 →](stap4-k3s.md)
