# Traefik

## 🔧 Overview

**Traefik** is the reverse proxy and router for local services. It handles container discovery and routes requests internally (LAN) and optionally externally.

---

## 🧱 Deployment

| Parameter            | Value                    |
|---------------------|--------------------------|
| Host                | ruby-z04-node-s01        |
| Container Runtime   | Docker                   |
| Network             | bridge (`br0`)           |
| Config Dir          | `/opt/data/traefik/`     |
| Entrypoints         | 80 (http), 443 (https)   |

---

## 🗂️ Configuration

- `traefik.yml` defines static config
- Dynamic routers and services defined via `dynamic/` directory
- Docker labels drive service routing

---

## 🔐 Security

- Dashboard access protected via Basic Auth
- Future upgrade to Vault-sourced secrets and mTLS
- Not publicly exposed by default (but supports selective WAN exposure)

---

## 🌐 DNS / Routing

Routes requests such as:
- `vault.rutabagel.com` → Vaultwarden
- `home.rutabagel.com` → (planned) HAOS VM bridge

---

## 🔄 Pattern

Uses Docker labels like:

```yaml
labels:
  - "traefik.http.routers.vaultwarden.rule=Host(`vault.rutabagel.com`)"
  - "traefik.http.routers.vaultwarden.entrypoints=websecure"
  - "traefik.http.routers.vaultwarden.tls=true"
```
