# Stap 10 — Wachtwoord resetten

[← Stap 9](stap9-toegang.md) | [← Terug naar README](../README.md)

---

## Uitleg

Als het Rancher-wachtwoord vergeten is, kan het worden gereset via `kubectl` op de master node. Rancher heeft hiervoor een ingebouwd reset-commando beschikbaar via de pod zelf.

---

## Wachtwoord resetten

```bash
kubectl exec -n cattle-system -it \
  $(kubectl get pods -n cattle-system \
  -l app=rancher \
  --no-headers \
  -o custom-columns=":metadata.name" \
  | head -1) \
  -- reset-password
```

De uitvoer toont een nieuw willekeurig wachtwoord:

```
New password for default administrator (user-xxxxx):
<NIEUW WILLEKEURIG WACHTWOORD>
```

> ⚠️ **Kopieer het wachtwoord direct!** Het wordt maar één keer getoond. Log daarna meteen in via `https://192.168.1.104` en wijzig het naar iets memorabels.

---

## Wat doet dit commando?

| Onderdeel | Uitleg |
|---|---|
| `kubectl get pods -n cattle-system -l app=rancher` | Zoekt de naam van de actieve Rancher-pod op |
| `--no-headers -o custom-columns=":metadata.name"` | Geeft alleen de podnaam terug, zonder opmaak |
| `head -1` | Neemt alleen de eerste pod (bij meerdere replicas) |
| `kubectl exec -it ... -- reset-password` | Voert het reset-commando uit binnen de pod zelf |

---

[← Stap 9](stap9-toegang.md) | [← Terug naar README](../README.md)
