# 10. Toegang tot het Rancher-dashboard

Rancher is direct bereikbaar via het IP-adres van de master node — geen hosts-bestand aanpassen nodig.

---

## 10.1 Dashboard openen

Open een browser en ga naar:

```
https://192.168.1.104
```

> ⚠️ **SSL-certificaatwaarschuwing**
> De browser toont waarschijnlijk een certificaatwaarschuwing omdat het certificaat zelfondertekend (self-signed) is.
> Klik op **Geavanceerd** → **Doorgaan naar 192.168.1.104**.
> In een productieomgeving gebruik je een certificaat van Let's Encrypt.

---

## 10.2 Inloggen

| Veld | Waarde |
|---|---|
| URL | `https://192.168.1.104` |
| Gebruikersnaam | `admin` |
| Wachtwoord | `JouwWachtwoord123` (ingesteld bij helm install) |

Na het eerste inloggen vraagt Rancher je het wachtwoord te wijzigen. Kies een sterk wachtwoord en sla het op in een wachtwoordmanager.

---

## ✅ Rancher is nu operationeel!

Via de webinterface kun je nu:

- Kubernetes-workloads deployen
- Pods en services beheren
- Resources monitoren (CPU, RAM, opslag)
- Namespaces aanmaken en beheren
- Helm-charts installeren via de UI

---

[← Vorige: Rancher installeren](09-rancher-installeren.md) | [Volgende: Wachtwoord resetten →](11-wachtwoord-resetten.md)
