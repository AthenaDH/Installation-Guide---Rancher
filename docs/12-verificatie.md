# 12. Eindverificatie

Voer de volgende commando's uit om te bevestigen dat alles correct geïnstalleerd is.

---

## Cluster status

```bash
# Alle nodes controleren
kubectl get nodes

# Alle pods in alle namespaces
kubectl get pods -A

# Alle geïnstalleerde Helm-releases
helm list -A
```

---

## Verwachte uitvoer — `kubectl get nodes`

```
NAME          STATUS   ROLES                  AGE   VERSION
k3s-master    Ready    control-plane,master   10m   v1.34.5+k3s1
k3s-worker1   Ready    <none>                 5m    v1.34.5+k3s1
k3s-worker2   Ready    <none>                 4m    v1.34.5+k3s1
```

---

## Verwachte uitvoer — `helm list -A`

| Naam | Namespace | Status | Chart |
|---|---|---|---|
| longhorn | longhorn-system | deployed | longhorn-1.x.x |
| rancher | cattle-system | deployed | rancher-2.x.x |

---

## Checklist

- [ ] Alle drie nodes tonen `STATUS: Ready`
- [ ] Longhorn StorageClass aanwezig als `default`
- [ ] cert-manager pods: `Running`
- [ ] Rancher pod: `Running`
- [ ] Dashboard bereikbaar op `https://192.168.1.104`
- [ ] Inloggen met admin-account lukt

---

## Overzicht geïnstalleerde componenten

| Component | Namespace | Doel |
|---|---|---|
| k3s cluster | — | Lichtgewicht Kubernetes-cluster |
| Helm v3 | — | Package manager voor Kubernetes |
| Longhorn | `longhorn-system` | Persistente gedistribueerde opslag |
| cert-manager | `cert-manager` | Automatisch SSL-certificaatbeheer |
| Rancher | `cattle-system` | Grafisch beheerdashboard |

---

[← Vorige: Wachtwoord resetten](11-wachtwoord-resetten.md) | [↑ Terug naar begin](../README.md)
