# 9. Rancher installeren

Nu alle vereisten aanwezig zijn kan Rancher geïnstalleerd worden via de officiële Helm-chart.

---

## 9.1 Helm-repository toevoegen

```bash
helm repo add rancher-stable \
  https://releases.rancher.com/server-charts/stable
helm repo update
```

> 💡 `rancher-stable` wordt aanbevolen voor schoolomgevingen — uitgebreid getest en minder kans op onverwachte problemen dan `rancher-latest`.

---

## 9.2 Namespace aanmaken

```bash
kubectl create namespace cattle-system
```

---

## 9.3 Rancher installeren

```bash
helm install rancher rancher-stable/rancher \
  --namespace cattle-system \
  --set hostname=192.168.1.104 \
  --set replicas=1 \
  --set bootstrapPassword=JouwWachtwoord123
```

| Parameter | Uitleg |
|---|---|
| `--namespace cattle-system` | Rancher wordt geïsoleerd in zijn eigen namespace |
| `--set hostname=192.168.1.104` | IP-adres waarmee Rancher bereikbaar is |
| `--set replicas=1` | Één instantie — voldoende voor lab/school |
| `--set bootstrapPassword` | Initieel wachtwoord voor de admin-gebruiker |

---

## 9.4 Installatie volgen

```bash
kubectl get pods -n cattle-system -w
```

Wacht tot alle pods `Running` zijn (3–5 minuten):

```
NAME                READY   STATUS    RESTARTS
rancher-xxxx-xxxx   1/1     Running   0
rancher-xxxx-xxxx   1/1     Running   0
```

---

[← Vorige: cert-manager](08-cert-manager.md) | [Volgende: Toegang tot Rancher →](10-toegang.md)
