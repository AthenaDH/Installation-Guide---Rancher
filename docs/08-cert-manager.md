# 8. cert-manager installeren

cert-manager is een Kubernetes-add-on die automatisch TLS/SSL-certificaten aanmaakt en vernieuwt. Rancher vereist cert-manager om zijn eigen HTTPS-certificaat te genereren.

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

Controleer alle pods:

```bash
kubectl get pods -n cert-manager
```

Verwachte uitvoer:

```
NAME                                      READY   STATUS
cert-manager-xxxx                         1/1     Running
cert-manager-cainjector-xxxx              1/1     Running
cert-manager-webhook-xxxx                 1/1     Running
```

---

[← Vorige: Longhorn](07-longhorn-installeren.md) | [Volgende: Rancher installeren →](09-rancher-installeren.md)
