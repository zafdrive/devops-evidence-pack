# DevOps Evidence Pack (Production-like Platform on a VPS)

This repository is the entry point to my DevOps/Infrastructure portfolio: a production-like Kubernetes platform running on a single Ubuntu VPS (k3s) with GitOps, CI/CD, observability, logging, and backup/restore drills.

**Owner:** Pablo Comas Herrera  
**Portfolio:** https://zafdrive.com  
**Contact:** pablocomas@zafdrive.com | LinkedIn: https://linkedin.com/in/pablo-comas

---

## Live demo (public)

- App: https://app.<YOUR_DOMAIN>
- API health: https://api.<YOUR_DOMAIN>/health
- Status: https://status.<YOUR_DOMAIN>

> Argo CD and Grafana are intentionally **not public**. They are available only via VPN/IP allowlist for security.

---

## What I built (high level)

- **Kubernetes (k3s)** single-node cluster on an Ubuntu VPS
- **GitOps** deployments with Argo CD (source of truth = Git)
- **CI/CD** with GitHub Actions: test → build → push image → update GitOps → rollout
- **Observability** with Prometheus + Grafana (dashboards + alerting)
- **Centralized logging** with Loki (logs per namespace/app)
- **Backup & restore drill** for PostgreSQL with measured RTO/RPO
- **Runbooks** and a simulated incident / postmortem (GameDay)

---

## Architecture

![Architecture](docs/architecture.png)

If the image is missing, see: `docs/architecture.drawio` (source).

---

## Repositories (modules)

- GitOps (k3s + Argo CD manifests):  
  https://github.com/<YOUR_GH_USER>/gitops-k3s-argocd

- Demo application (FastAPI, metrics, health checks):  
  https://github.com/<YOUR_GH_USER>/demo-fastapi-app

- Observability (kube-prometheus-stack, dashboards, alerts):  
  https://github.com/<YOUR_GH_USER>/observability-stack

- Backup & restore drill (PostgreSQL → S3/MinIO, runbook):  
  https://github.com/<YOUR_GH_USER>/backup-restore-drill

---

## Proof / screenshots

I will keep adding screenshots and short demos as the platform evolves.

- [ ] Argo CD “Healthy/Synced” view
- [ ] CI pipeline successful run + auto PR to GitOps repo
- [ ] Grafana dashboard (RPS/latency/errors + node/container)
- [ ] Backup + restore logs and verification

Screenshots live in: `docs/screenshots/`

---

## How to reproduce (overview)

This is the minimal reproducible flow (details live in each module repo):

1. Provision an Ubuntu VPS and configure DNS for `app/api/status` subdomains.
2. Install k3s and kubectl access.
3. Install Argo CD in-cluster.
4. Bootstrap GitOps (“app-of-apps”) pointing to `gitops-k3s-argocd`.
5. Push code changes to `demo-fastapi-app` → GitHub Actions builds and pushes images.
6. CI updates the image tag in GitOps repo → Argo CD sync deploys it.

---

## Security notes

- No credentials are stored in Git.
- Argo CD and Grafana endpoints are restricted via VPN or IP allowlist.
- Any public endpoints are protected by TLS (via reverse proxy) and minimal exposure.

---

## Roadmap

See `ROADMAP.md` for the 8-week plan and milestones.

---

## License

MIT License.
