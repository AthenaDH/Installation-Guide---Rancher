# 6. Helm installeren

Helm is de package manager voor Kubernetes — vergelijkbaar met `apt` voor Debian. Met Helm installeer je complexe applicaties via voorgedefinieerde configuratiepakketten genaamd *charts*.

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

Verifieer:

```bash
helm version
```

Verwachte uitvoer:

```
version.BuildInfo{Version:"v3.x.x", ...}
```

---

[← Vorige: k3s installeren](05-k3s-installeren.md) | [Volgende: Longhorn installeren →](07-longhorn-installeren.md)
