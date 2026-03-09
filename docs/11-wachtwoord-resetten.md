# 11. Wachtwoord resetten

Als het Rancher-wachtwoord vergeten is, kan het worden gereset via `kubectl` op de master node. Rancher heeft hiervoor een ingebouwd reset-commando.

---

## Commando

```bash
kubectl exec -n cattle-system -it \
  $(kubectl get pods -n cattle-system \
  -l app=rancher \
  --no-headers \
  -o custom-columns=":metadata.name" \
  | head -1) \
  -- reset-password
```

---

## Uitvoer

```
New password for default administrator (user-xxxxx):
<NIEUW WILLEKEURIG WACHTWOORD>
```

> ⚠️ Het wachtwoord wordt maar **één keer** getoond.
> Log daarna meteen in via `https://192.168.1.104` en wijzig het naar iets memorabels.
> Sla alle wachtwoorden op in een wachtwoordmanager.

---

[← Vorige: Toegang](10-toegang.md) | [Volgende: Eindverificatie →](12-verificatie.md)
