# Stap 6 — Longhorn installeren

[← Stap 5](stap5-helm.md) | [Stap 7 →](stap7-certmanager.md)

---

## Uitleg

Longhorn is een gedistribueerd opslagsysteem voor Kubernetes. Zonder Longhorn gaat alle data verloren zodra een pod herstart.

**Waarom is dit nodig?**

Kubernetes pods zijn van nature stateless (tijdelijk). Bij een crash start Kubernetes een nieuwe pod — volledig leeg. Longhorn koppelt een `PersistentVolume` aan de pod. Die schijf blijft bestaan, ongeacht hoeveel keer de pod herstart. Rancher slaat zijn eigen configuratie ook op via een `PersistentVolumeClaim`.

Longhorn repliceert data over meerdere worker nodes (`defaultReplicaCount=2`), zodat bij uitval van één worker de data nog steeds beschikbaar is.

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

Wacht tot alle pods draaien (2–3 minuten):

```bash
kubectl get pods -n longhorn-system -w
```

Druk op `CTRL+C` zodra alle pods `Running` tonen.

---

## Verificatie

Controleer of de StorageClass aangemaakt is:

```bash
kubectl get storageclass
```

Verwachte uitvoer:

```
NAME                 PROVISIONER          RECLAIMPOLICY   VOLUMEBINDINGMODE
longhorn (default)   driver.longhorn.io   Delete          Immediate
```

> ✅ `(default)` betekent dat Longhorn automatisch gebruikt wordt voor alle PersistentVolumeClaims.

---

[← Stap 5](stap5-helm.md) | [Stap 7 →](stap7-certmanager.md)
