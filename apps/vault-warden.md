# Vaultwarden

## 🔧 Overview

**Vaultwarden** is a lightweight Bitwarden-compatible password manager. It’s deployed in Docker and secured with Traefik as the reverse proxy.

Accessible at:
```
https://vault.rutabagel.com
```

---

## 🧱 Deployment

| Parameter            | Value                    |
|---------------------|--------------------------|
| Host                | ruby-z04-node-s01        |
| Container Runtime   | Docker                   |
| Network             | Custom bridge (`br0`)    |
| Data Dir            | `/opt/data/vaultwarden/` |
| Domain              | `vault.rutabagel.com`    |

---

## 🔐 Secrets

- SMTP credentials injected via `.env` (Vault-managed)
- Admin token stored in Vault (not in compose)

---

## 🔒 Reverse Proxy

- Handled by Traefik
- TLS enabled (Let's Encrypt not used — LAN only)
- Basic Auth enforced at router level
