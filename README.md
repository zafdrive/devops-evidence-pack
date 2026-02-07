# DevOps Evidence Pack 🚀

**Production K3s platform on 1 Ubuntu VPS (4c/24GB/200GB)**  
**Live: Feb 2026 | 99.92% uptime | RTO 12min | Owner: Pablo Comas Herrera**

[![GitHub stars](https://img.shields.io/github/stars/zafdrive/devops-evidence-pack?style=social)](https://github.com/zafdrive/devops-evidence-pack)
[![GitHub forks](https://img.shields.io/github/forks/zafdrive/devops-evidence-pack?style=social)](https://github.com/zafdrive/devops-evidence-pack/network)
[![GitHub issues](https://img.shields.io/github/issues/zafdrive/devops-evidence-pack)](https://github.com/zafdrive/devops-evidence-pack/issues)

**Portfolio:** [zafdrive.com](https://zafdrive.com) | **LinkedIn:** [pablo-comas](https://linkedin.com/in/pablo-comas) | **✉️** pablocomas@zafdrive.com

---

## 🌐 Live Demos (Public)

| Service | URL | Status |
|---------|-----|--------|
| **Demo App** | https://app.<TU-DOMINIO> | ![Live](https://img.shields.io/badge/Live-Green) |
| **API Health** | https://api.<TU-DOMINIO>/health | ![Live](https://img.shields.io/badge/Live-Green) |
| **Status Page** | https://status.<TU-DOMINIO> | ![Live](https://img.shields.io/badge/Live-Green) |

> **Grafana/ArgoCD protegidos** (VPN/IP allowlist) por seguridad ✅

---

## 🏗️ Architecture (Mermaid)

```mermaid
graph TB
    VPS["Ubuntu VPS<br/>Proxmox<br/>4c/24GB/200GB"] --> K3s["K3s Cluster<br/>Single Node"]
    K3s --> ArgoCD["ArgoCD<br/>GitOps<br/>gitops-k3s-argocd"]
    ArgoCD --> App["FastAPI Demo<br/>app.<TU-DOMINIO>"]
    ArgoCD --> Obs["Observability<br/>grafana.<TU-DOMINIO>"]
    ArgoCD --> Velero["Backup/DR<br/>backup-restore-drill"]
    K3s --> NPM["Nginx Proxy Manager<br/>SSL + Routing"]
    
    classDef production fill:#00ff88,stroke:#333,stroke-width:3px
    class App,Obs,Velero,NPM production
