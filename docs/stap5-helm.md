# Stap 5 — Helm installeren

[← Stap 4](stap4-k3s.md) | [Stap 6 →](stap6-longhorn.md)

---

## Uitleg

Helm is de package manager voor Kubernetes — vergelijkbaar met `apt` voor Debian. Met Helm installeer je complexe applicaties via zogenaamde **charts**: voorgedefinieerde configuratiepakketten. Rancher, Longhorn en cert-manager worden allemaal via Helm geïnstalleerd.

---

## Installatie

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

Verifieer de installatie:

```bash
helm version
```

Verwachte uitvoer:

```
version.BuildInfo{Version:"v3.x.x", ...}
```

---

[← Stap 4](stap4-k3s.md) | [Stap 6 →](stap6-longhorn.md)
