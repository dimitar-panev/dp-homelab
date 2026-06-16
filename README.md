# Homelab Infrastructure & Docker Stack

A modular, self-hosted homelab infrastructure deployed on an Ubuntu virtual machine via Proxmox. This repository contains the Docker Compose configurations and deployment structures for my core network services.

## 👨‍💻 About
Maintained by **Le Me** with the idea of integrating more stuff into this project of mine. I am currently looking into terraform so maybe I could implement it here as well. 

## 🏗️ Architecture & Philosophy

This homelab utilizes a modular Docker design. Rather than a single monolithic `docker-compose.yml`, every service is strictly isolated in its own directory. 

* **Isolation:** Each service runs its own compose stack, allowing independent updates and restarts without bringing down the entire environment.
* **Security First:** Secrets, API keys, and environment variables are strictly kept out of version control. Configuration relies on local `.env` files securely injected into containers at runtime.
* **State Management:** Application states (SQLite databases, proxy logs, custom SSL certificates, and user uploads) are persistently mapped to local volumes but universally ignored via `.gitignore` to prevent accidental public exposure.

## 🚀 Services Deployed

* **[Homepage](https://gethomepage.dev/):** A modern, fully static, secure custom application dashboard. Integrates via API with Proxmox, NextDNS, and local network monitors.
* **[Nginx Proxy Manager](https://nginxproxymanager.com/):** The core reverse proxy handling traffic routing, local DNS resolution, and automated Let's Encrypt SSL certificate provisioning.
* **[Pingvin Share](https://github.com/stonith404/pingvin-share):** A self-hosted, privacy-focused alternative for secure file sharing.
* **[Speedtest Tracker](https://github.com/alexjustesen/speedtest-tracker):** Automated network performance monitoring and logging.
* **[IT-Tools](https://it-tools.tech/):** A lightweight collection of handy developer and sysadmin tools.

## 📂 Directory Structure

The repository reflects the exact infrastructure state minus sensitive data:

```text
.
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
├── it-tools/
│   └── docker-compose.yml
├── npm/
│   └── docker-compose.yml
├── pingvin/
│   └── docker-compose.yml
└── speedtest-tracker/
    ├── config/
    │   ├── nginx/
    │   ├── php/
    │   └── www/
    └── docker-compose.yaml
