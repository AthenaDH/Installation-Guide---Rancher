# Stap 4 — k3s installeren

[← Stap 3](stap3-voorbereiding.md) | [Stap 5 →](stap5-helm.md)

---

## 4.1 Master node installeren

Voer dit uit op de **master node** (192.168.1.104):

```bash
curl -sfL https://get.k3s.io | sh -
```

Het script installeert k3s als een systemd-service en start het automatisch. Controleer de status:

```bash
systemctl status k3s
```

---

## 4.2 kubeconfig instellen

kubectl heeft een configuratiebestand nodig om te weten met welk cluster het moet verbinden. k3s slaat dit op in een niet-standaard locatie:

```bash
export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
echo "export KUBECONFIG=/etc/rancher/k3s/k3s.yaml" >> ~/.bashrc
echo "export KUBECONFIG=/etc/rancher/k3s/k3s.yaml" >> /home/JOUWGEBRUIKER/.bashrc
source ~/.bashrc
```

---

## 4.3 Master node verifiëren

```bash
kubectl get nodes
```

Verwachte uitvoer:

```
NAME        STATUS   ROLES                  AGE   VERSION
k3s-master  Ready    control-plane,master   1m    v1.34.5+k3s1
```

---

## 4.4 Node token opslaan

De worker nodes hebben een token nodig om lid te worden van het cluster. Sla dit op:

```bash
cat /var/lib/rancher/k3s/server/node-token
```

> ⚠️ **Sla dit token op!** Je hebt het nodig in stap 4.6.

---

## 4.5 Hostnaam aanpassen op workers

Na het klonen van de master VM pas je de hostnaam aan op elke worker:

```bash
# Op k3s-worker1:
hostnamectl set-hostname k3s-worker1

# Op k3s-worker2:
hostnamectl set-hostname k3s-worker2
```

---

## 4.6 Workers toevoegen aan het cluster

Voer dit uit op **beide worker nodes** — vervang de placeholders:

```bash
curl -sfL https://get.k3s.io | \
  K3S_URL=https://192.168.1.104:6443 \
  K3S_TOKEN=PLAK-TOKEN-HIER \
  sh -
```

Controleer de agent status op de worker:

```bash
systemctl status k3s-agent
```

---

## 4.7 Cluster verifiëren

Terug op de **master node**:

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

[← Stap 3](stap3-voorbereiding.md) | [Stap 5 →](stap5-helm.md)
