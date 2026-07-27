# ⚡ Homelab Infrastructure & Docker Stack

A modular, self-hosted homelab infrastructure deployed on an Ubuntu virtual machine via Proxmox. This repository contains the Docker Compose configurations, environmental templates, and deployment structures for my core network services.

## 👨‍💻 About
Maintained by **Dimitar Panev**. This repository is continuously evolving as I integrate new services and optimize the infrastructure. Currently focusing on expanding automation capabilities and exploring Infrastructure as Code (IaC) with Terraform.

---

## 🏗️ Architecture & Philosophy

This homelab utilizes a strictly modular Docker design. Rather than relying on a single monolithic `docker-compose.yml`, every service is isolated in its own directory. 

* **Isolation:** Each service runs its own compose stack, allowing for independent updates, rollbacks, and restarts without impacting the broader environment.
* **Security First:** Secrets, API keys, and environment variables are strictly kept out of version control. Configuration relies on local `.env` files securely injected into containers at runtime.
* **State Management:** Application states (databases, proxy logs, custom SSL certificates, and user uploads) are persistently mapped to local volumes but universally ignored via `.gitignore` to prevent accidental public exposure.

---

## 🚀 Services Deployed

### Core Management & Routing
* **[Dockge](https://dockge.kuma.pet/):** A reactive, web-based GUI for managing, creating, and updating Docker Compose stacks.
* **[Nginx Proxy Manager](https://nginxproxymanager.com/):** The core reverse proxy handling traffic routing, local DNS resolution, and automated Let's Encrypt SSL certificate provisioning.

### Monitoring & Analytics
* **[Homepage](https://gethomepage.dev/):** A modern, fully static, secure custom application dashboard. Integrates via API with Proxmox, NextDNS, and local network monitors.
* **[InfluxDB](https://www.influxdata.com/):** A high-performance time-series database utilized for storing homelab metrics and network telemetry.
* **[Grafana](https://grafana.com/):** The primary visualization platform connected to InfluxDB for building detailed infrastructure observability dashboards.
* **[Speedtest Tracker](https://github.com/alexjustesen/speedtest-tracker):** Automated network performance monitoring and historical logging.

### Utilities & Productivity
* **[Pingvin Share](https://github.com/stonith404/pingvin-share):** A self-hosted, privacy-focused alternative for secure file sharing.
* **[Stirling-PDF](https://github.com/Stirling-Tools/Stirling-PDF):** A robust, locally hosted web application for manipulating, merging, and modifying PDF files securely.
* **[IT-Tools](https://it-tools.tech/):** A lightweight, comprehensive collection of handy developer and sysadmin tools.

---

## 🗺️ Roadmap & Future Implementations

As this infrastructure evolves, the following technologies and architectural improvements are slated for deployment:

* **Infrastructure as Code (IaC):** Implementing Terraform to manage the Proxmox hypervisor layer and automate the provisioning of future Ubuntu VMs, LXC containers, and network state.
* **Advanced Alerting:** Deploying Prometheus and Alertmanager to establish threshold-based alerts for container health and hardware metrics.
* **Identity Provider (SSO):** Integrating Authentik or Authelia behind Nginx Proxy Manager to enforce strict 2FA (Two-Factor Authentication) across all externally exposed web services.

---

## 📂 Directory Structure

The repository reflects the exact infrastructure state minus sensitive data and local volumes:

```text
.
├── dockge/
│   └── docker-compose.yml
├── grafana/
│   └── docker-compose.yml
├── homepage/
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
│   └── docker-compose.yml
├── it-tools/
│   └── docker-compose.yml
├── npm/
│   └── docker-compose.yml
├── pingvin/
│   └── docker-compose.yml
├── speedtest-tracker/
│   ├── config/
│   │   ├── nginx/
│   │   ├── php/
│   │   └── www/
│   └── docker-compose.yaml
└── stirling-pdf/
    └── docker-compose.yml
