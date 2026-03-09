# 4. Nodes voorbereiden voor Kubernetes

> ⚠️ Voer alle commando's op **elke node** uit — master én beide workers.

---

## 4.1 APT-bronnen bijwerken

```bash
nano /etc/apt/sources.list
```

Vervang de inhoud door:

```
deb http://deb.debian.org/debian bookworm main contrib non-free non-free-firmware
deb http://deb.debian.org/debian bookworm-updates main contrib non-free non-free-firmware
deb http://security.debian.org/debian-security bookworm-security main contrib non-free
```

```bash
apt update && apt upgrade -y
```

---

## 4.2 Benodigde pakketten installeren

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
| `net-tools` | Netwerkdiagnostiek |
| `sudo` | Verhoogde rechten voor gewone gebruiker |
| `qemu-guest-agent` | Communicatie tussen VM en Proxmox-host |

---

## 4.3 Swap uitschakelen

Kubernetes vereist dat swap uitgeschakeld is. Swap kan de scheduler in de war brengen omdat Kubernetes geheugenlimieten strikt beheert.

```bash
swapoff -a
sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
```

> 💡 De tweede regel zorgt dat swap ook na een herstart uitgeschakeld blijft door de swap-regel in `/etc/fstab` te commentariëren.

---

## 4.4 Kernelmodules laden

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
| `overlay` | Maakt overlay-filesystems mogelijk — hiermee werken container-images |
| `br_netfilter` | Laat iptables bridge-verkeer filteren — vereist voor pod-communicatie |

---

## 4.5 Netwerkinstellingen

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
| `bridge-nf-call-iptables` | Zorgt dat gebridged verkeer door iptables gaat — vereist voor Kubernetes Services |
| `ip_forward` | Staat IP-forwarding toe tussen interfaces — pods kunnen anders niet communiceren |

---

[← Vorige: Debian installeren](03-debian-installeren.md) | [Volgende: k3s installeren →](05-k3s-installeren.md)
