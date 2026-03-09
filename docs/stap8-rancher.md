# Stap 8 — Rancher installeren

[← Stap 7](stap7-certmanager.md) | [Stap 9 →](stap9-toegang.md)

---

## 8.1 Helm-repository toevoegen

```bash
helm repo add rancher-stable \
  https://releases.rancher.com/server-charts/stable
helm repo update
```

> 💡 **rancher-stable** wordt gebruikt in plaats van `rancher-latest` — dit kanaal is uitgebreid getest en aanbevolen voor productie en schoolomgevingen.

---

## 8.2 Namespace aanmaken

```bash
kubectl create namespace cattle-system
```

---

## 8.3 Rancher installeren

```bash
helm install rancher rancher-stable/rancher \
  --namespace cattle-system \
  --set hostname=192.168.1.104 \
  --set replicas=1 \
  --set bootstrapPassword=JouwWachtwoord123
```

### Uitleg parameters

| Parameter | Waarde | Uitleg |
|---|---|---|
| `--namespace cattle-system` | `cattle-system` | Rancher wordt geïsoleerd in zijn eigen namespace |
| `--set hostname` | `192.168.1.104` | Het IP-adres waarmee Rancher bereikbaar is |
| `--set replicas=1` | `1` | Één instantie — voldoende voor lab/schoolomgeving |
| `--set bootstrapPassword` | `JouwWachtwoord123` | Initieel wachtwoord voor de admin-gebruiker |

---

## 8.4 Installatie volgen

Houd de voortgang bij — alle pods moeten `Running` worden (3–5 minuten):

```bash
kubectl get pods -n cattle-system -w
```

Verwachte uitvoer:

```
NAME                READY   STATUS    RESTARTS
rancher-xxxx-xxxx   1/1     Running   0
rancher-xxxx-xxxx   1/1     Running   0
```

Druk op `CTRL+C` zodra alle pods `Running` tonen.

---

[← Stap 7](stap7-certmanager.md) | [Stap 9 →](stap9-toegang.md)
