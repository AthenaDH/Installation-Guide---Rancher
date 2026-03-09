# 7. Longhorn installeren — persistente opslag

Longhorn is een gedistribueerd opslagsysteem voor Kubernetes. Zonder Longhorn gaat alle data verloren zodra een pod herstart. Longhorn repliceert data over meerdere worker nodes zodat data bewaard blijft.

> 💡 **Waarom is dit nodig?**
> Kubernetes pods zijn van nature *stateless* (tijdelijk). Bij een herstart start Kubernetes een nieuwe pod — leeg. Longhorn koppelt een PersistentVolume aan de pod. Die schijf blijft bestaan, ongeacht hoeveel keer de pod herstart. Rancher slaat zijn eigen configuratie ook op via een PersistentVolumeClaim.

---

## Installatie

```bash
helm repo add longhorn https://charts.longhorn.io
helm repo update
kubectl create namespace longhorn-system

helm install longhorn longhorn/longhorn \
  --namespace longhorn-system \
  --set defaultSettings.defaultReplicaCount=2
```

> 💡 `defaultReplicaCount=2` betekent dat elke PVC over 2 worker nodes gerepliceerd wordt. Als één worker uitvalt, blijft de data bereikbaar via de andere worker.

Wacht tot alle pods draaien (2–3 minuten):

```bash
kubectl get pods -n longhorn-system -w
```

Controleer of de StorageClass aangemaakt is:

```bash
kubectl get storageclass
# Verwachte uitvoer: longhorn (default)
```

---

[← Vorige: Helm installeren](06-helm-installeren.md) | [Volgende: cert-manager →](08-cert-manager.md)
