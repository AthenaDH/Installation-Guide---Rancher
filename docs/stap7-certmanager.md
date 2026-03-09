# Stap 7 — cert-manager installeren

[← Stap 6](stap6-longhorn.md) | [Stap 8 →](stap8-rancher.md)

---

## Uitleg

cert-manager is een Kubernetes-add-on die automatisch TLS/SSL-certificaten aanmaakt en vernieuwt. Rancher vereist cert-manager om zijn eigen HTTPS-certificaat te genereren. Zonder cert-manager weigert Rancher te starten.

---

## Installatie

```bash
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.14.0/cert-manager.yaml
```

Wacht tot cert-manager volledig operationeel is:

```bash
kubectl wait --for=condition=ready pod \
  -l app=cert-manager \
  -n cert-manager \
  --timeout=120s
```

---

## Verificatie

```bash
kubectl get pods -n cert-manager
```

Verwachte uitvoer — alle drie pods moeten `Running` zijn:

```
NAME                                      READY   STATUS
cert-manager-xxxx                         1/1     Running
cert-manager-cainjector-xxxx              1/1     Running
cert-manager-webhook-xxxx                 1/1     Running
```

---

[← Stap 6](stap6-longhorn.md) | [Stap 8 →](stap8-rancher.md)
