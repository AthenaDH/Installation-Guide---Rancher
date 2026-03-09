# 5. k3s installeren en cluster opbouwen

k3s wordt geïnstalleerd via een officieel installatiescript. Het script detecteert automatisch het besturingssysteem, downloadt de juiste binaries en configureert de systemd-service.

---

## 5.1 Master node installeren

Voer dit uit op de master node (`192.168.1.104`):

```bash
curl -sfL https://get.k3s.io | sh -
```

Controleer de status:

```bash
systemctl status k3s
```

---

## 5.2 kubeconfig instellen

`kubectl` heeft een configuratiebestand nodig om te weten met welk cluster het moet verbinden. k3s slaat dit op in een niet-standaard locatie:

```bash
export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
echo "export KUBECONFIG=/etc/rancher/k3s/k3s.yaml" >> ~/.bashrc
echo "export KUBECONFIG=/etc/rancher/k3s/k3s.yaml" >> /home/JOUWGEBRUIKER/.bashrc
source ~/.bashrc
```

---

## 5.3 Master node verifiëren

```bash
kubectl get nodes
```

Verwachte uitvoer:

```
NAME        STATUS   ROLES                  AGE   VERSION
k3s-master  Ready    control-plane,master   1m    v1.34.5+k3s1
```

---

## 5.4 Node token ophalen

> ⚠️ Sla dit token op — de workers hebben het nodig om lid te worden van het cluster!

```bash
cat /var/lib/rancher/k3s/server/node-token
```

---

## 5.5 Worker nodes klonen

In Proxmox kun je de master-VM klonen:

```
Klik rechts op k3s-master → Clone
  VM ID: 102 | Naam: k3s-worker1 | Mode: Full Clone

Klik rechts op k3s-master → Clone
  VM ID: 103 | Naam: k3s-worker2 | Mode: Full Clone
```

Verhoog daarna het RAM van beide workers:
```
Hardware → Memory → 16384 MB
```

Pas de hostnaam aan op elke worker na opstarten:

```bash
# Op k3s-worker1:
hostnamectl set-hostname k3s-worker1

# Op k3s-worker2:
hostnamectl set-hostname k3s-worker2
```

---

## 5.6 Workers toevoegen aan het cluster

Voer dit uit op **beide** worker nodes:

```bash
curl -sfL https://get.k3s.io | \
  K3S_URL=https://192.168.1.104:6443 \
  K3S_TOKEN=PLAK-TOKEN-HIER \
  sh -
```

---

## 5.7 Cluster verifiëren

Terug op de master node:

```bash
kubectl get nodes
```

Verwachte uitvoer — alle drie nodes moeten `Ready` zijn:

```
NAME          STATUS   ROLES                  AGE   VERSION
k3s-master    Ready    control-plane,master   10m   v1.34.5+k3s1
k3s-worker1   Ready    <none>                 2m    v1.34.5+k3s1
k3s-worker2   Ready    <none>                 1m    v1.34.5+k3s1
```

---

[← Vorige: Nodes voorbereiden](04-nodes-voorbereiden.md) | [Volgende: Helm installeren →](06-helm-installeren.md)
