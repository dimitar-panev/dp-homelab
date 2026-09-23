# ⚡ Homelab Infrastructure & Docker Stack

A modular self-hosted homelab infrastructure deployed on an Ubuntu virtual machine via Proxmox. This repository contains the Docker Compose configurations alongside the environmental templates for my core network services.

## 👨‍💻 About
Maintained by **Dimitar Panev**. This repository continuously evolves as I integrate new services. I am currently focusing on expanding automation capabilities. Another major goal involves exploring Infrastructure as Code (IaC) with Terraform.

---

## 🏗️ Architecture & Philosophy

This homelab utilizes a strictly modular Docker design fortified by rigorous network and host-level security. Every service operates independently within its own dedicated directory.

* **Network Isolation:** Containers are attached to an isolated custom external Docker bridge (`proxy-net`). Host port bindings are explicitly removed across all application stacks to prevent direct IP access.
* **Internal Routing & ACLs:** Nginx Proxy Manager (NPM) exclusively handles all external traffic. NPM resolves services via Docker's internal DNS using the `container_name` parameter. Administrative dashboards remain locked behind Subnet Access Control Lists (ACLs). These lists restrict access solely to the local `172.16.175.0/24` subnet.
* **Security First:** The Ubuntu host is hardened with UFW allowing only specific ports like 22 or 443. Fail2Ban provides automated SSH intrusion prevention. SSH access requires strict ED25519 cryptographic keys. Password authentication is entirely disabled.
* **Centralized Environment Variables:** Secrets are kept out of version control. Configuration relies on a centralized global `.env` file at the repository root. This file is securely injected into individual containers at runtime via symlinks (`ln -s ../.env .env`).
* **State Management:** Application states like live databases, proxy logs, custom SSL certificates, and user uploads are persistently mapped to local volumes. A robust `.gitignore` universally hides these elements to prevent accidental public exposure.

---

## 🚀 Services Deployed

### Core Management & Routing
* **[Dockge](https://dockge.kuma.pet/):** A reactive web-based GUI for managing and updating Docker Compose stacks.
* **[Nginx Proxy Manager](https://nginxproxymanager.com/):** The core reverse proxy handling traffic routing and internal DNS resolution.

### Monitoring & Analytics
* **[Homepage](https://gethomepage.dev/):** A modern static custom application dashboard. It integrates via API with Proxmox and NextDNS.
* **[InfluxDB](https://www.influxdata.com/):** A high-performance time-series database utilized for storing homelab metrics.
* **[Grafana](https://grafana.com/):** The primary visualization platform connected to InfluxDB for building detailed infrastructure observability dashboards.
* **[Speedtest Tracker](https://github.com/alexjustesen/speedtest-tracker):** Automated network performance monitoring and historical logging.

### Utilities & Productivity
* **[Pingvin Share](https://github.com/stonith404/pingvin-share):** A self-hosted privacy-focused alternative for secure file sharing.
* **[Stirling-PDF](https://github.com/Stirling-Tools/Stirling-PDF):** A robust locally hosted web application for manipulating and modifying PDF files securely.
* **[IT-Tools](https://it-tools.tech/):** A lightweight comprehensive collection of handy developer and sysadmin tools.

---

## 🗺️ Roadmap & Future Implementations

As this infrastructure evolves, the following technologies are slated for deployment:

* **Infrastructure as Code (IaC):** Implementing Terraform to manage the Proxmox hypervisor layer. This will automate the provisioning of future Ubuntu VMs and LXC containers.
* **Advanced Alerting:** Deploying Prometheus and Alertmanager to establish threshold-based alerts for container health.
* **Identity Provider (SSO):** Integrating Authentik or Authelia behind Nginx Proxy Manager. This setup enforces strict 2FA (Two-Factor Authentication) across all externally exposed web services.

---

## 📂 Directory Structure

The repository reflects the exact infrastructure state minus sensitive data, centralized global variables, and local volumes:

```text
.
├── .env (Ignored via .gitignore)
├── .gitignore
├── dockge/
│   ├── .env -> ../.env (Symlink)
│   └── docker-compose.yml
├── grafana/
│   ├── .env -> ../.env
│   └── docker-compose.yml
├── homepage/
│   ├── .env -> ../.env
│   ├── config/
│   │   ├── bookmarks.yaml
│   │   ├── custom.css
│   │   ├── custom.js
│   │   ├── docker.yaml
│   │   ├── kubernetes.yaml
│   │   ├── proxmox.yaml
│   │   ├── services.yaml
│   │   ├── settings.yaml
│   │   └── widgets.yaml
│   └── docker-compose.yml
├── influxdb/
│   ├── .env -> ../.env
│   └── docker-compose.yml
├── it-tools/
│   ├── .env -> ../.env
│   └── docker-compose.yml
├── npm/
│   ├── .env -> ../.env
│   └── docker-compose.yml
├── pingvin/
│   ├── .env -> ../.env
│   └── docker-compose.yml
├── speedtest-tracker/
│   ├── .env -> ../.env
│   ├── config/
│   │   ├── nginx/
│   │   ├── php/
│   │   └── www/
│   └── docker-compose.yaml
└── stirling-pdf/
    ├── .env -> ../.env
    └── docker-compose.yml
