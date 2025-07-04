# `ruby-z04-node-s01`: Docker Orchestration

This document defines the container orchestration strategy for `ruby-z04-node-s01`, a general-purpose utility node that serves as the primary host for core infrastructure services in the homelab.

For system-level details (hardware, OS, host-level configuration), see [`config/ruby-z04-node-s01.md`](../config/ruby-z04-node-s01.md).

---

## 🐳 Docker Environment

- **Engine**: Docker CE (installed via convenience script)
- **Compose**: Docker Compose v2
- **Default bridge**: Disabled
- **Custom bridge**: `br0` (created and brought up via `force-br0-up.service`)
- **Container network strategy**:
  - `br0`: Used for most containers requiring static DHCP IPs
  - `host`: Used selectively (e.g., for Vault)
  - Named bridge networks (e.g., `homelab_lan`) may be created for inter-container communication where needed

---

## 📦 Container Structure

Each service is deployed via its own Docker Compose stack under:

```
/opt/services/<service-name>/docker-compose.yml
```

Persistent data is mounted via bind mounts in:

```
/opt/data/<service-name>/
```

For example:

- `/opt/services/vaultwarden/docker-compose.yml`
- `/opt/data/vaultwarden/`

---

## 🔗 Hosted Services

| Service            | Network Mode | Status             | Notes                                   |
|--------------------|--------------|---------------------|------------------------------------------|
| **Traefik**        | `br0`        | ✅ Running          | Entry point and reverse proxy for services |
| **Vault**          | `host`       | ✅ Running          | Host mode used for low-level port access |
| **Vaultwarden**    | `br0`        | ✅ Running          | Managed password vault                   |
| **Home Assistant** | Planned VM   | 🔄 Pending Rebuild | Will be redeployed in HAOS VM           |

See individual service documentation under [`/apps`](../apps/) for per-app configuration and exposed ports:

- [`apps/home-assistant.md`](../apps/home-assistant.md)
- [`apps/traefik.md`](../apps/traefik.md)
- [`apps/vault.md`](../apps/vault.md)
- [`apps/vaultwarden.md`](../apps/vaultwarden.md)

---

## 🚦 Compose Behavior

Services are launched manually or via optional `systemd` units:

```ini
# /etc/systemd/system/docker-compose@<service>.service
[Unit]
Description=Docker Compose App - %i
Requires=docker.service
After=docker.service

[Service]
Type=oneshot
RemainAfterExit=yes
WorkingDirectory=/opt/containers/%i
ExecStart=/usr/bin/docker compose up -d
ExecStop=/usr/bin/docker compose down
TimeoutStartSec=0

[Install]
WantedBy=multi-user.target
```

To enable:
```bash
sudo systemctl enable --now docker-compose@vaultwarden.service
```

---

## 🔐 Security & Secrets

- All services are LAN-only
- Basic authentication and HTTPS enforced via Traefik
- Some secrets are currently stored in `.env` files
- Migration to **Vault Agent template injection** is planned

---

## 📋 Related Automation

- [Backups](/automation/backups.md): Service volumes backed up via rsync-based jobs (planned)
- [Monitoring](/automation/monitoring.md): Node exporter and health checks (planned)
- [CI/CD](/automation/cicd.md): Placeholder for future deployment automation

---

## ✅ Status

| Area                  | Status                |
|-----------------------|------------------------|
| Docker installed      | ✅ Complete             |
| Bridge configured     | ✅ `br0` via systemd     |
| Compose files live    | ✅ Under `/opt/containers` |
| Reverse proxy active  | ✅ LAN-only access      |
| Vaultwarden           | ✅ Containerized        |
| Vault (host network)  | ✅ Functional           |
| Home Assistant        | 🔄 Pending (HAOS in VM) |

