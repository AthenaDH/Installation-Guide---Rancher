# Stap 9 — Toegang tot het Rancher-dashboard

[← Stap 8](stap8-rancher.md) | [Stap 10 →](stap10-wachtwoord.md)

---

## Dashboard openen

Rancher is direct bereikbaar via het IP-adres van de master node. Open een browser en ga naar:

```
https://192.168.1.104
```

---

## SSL-certificaatwaarschuwing

De browser toont waarschijnlijk een certificaatwaarschuwing:

```
Uw verbinding is niet privé
```

Dit is normaal — het certificaat is zelfondertekend (self-signed) door cert-manager.

**Oplossing:**

```
Klik op "Geavanceerd" → "Doorgaan naar 192.168.1.104"
```

> 💡 In een productieomgeving gebruik je een certificaat van Let's Encrypt via een echte domeinnaam. Voor een lab/schoolomgeving is een self-signed certificaat voldoende.

---

## Inloggen

| Veld | Waarde |
|---|---|
| Gebruikersnaam | `admin` |
| Wachtwoord | `JouwWachtwoord123` (ingesteld bij `helm install`) |

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

[← Stap 8](stap8-rancher.md) | [Stap 10 →](stap10-wachtwoord.md)
