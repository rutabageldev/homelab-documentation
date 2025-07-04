# Vault

## 🔧 Overview

**HashiCorp Vault** provides centralized secrets management and is hosted on `ruby-z04-node-s01` using Docker in **host networking mode** for mTLS readiness and port consistency.

---

## 🧱 Deployment

| Parameter            | Value                    |
|---------------------|--------------------------|
| Host                | ruby-z04-node-s01        |
| Container Runtime   | Docker (host network)    |
| Data Dir            | `/opt/data/vault/`       |
| Port                | 8200                     |
| Access              | LAN-only (no WAN access) |

---

## 🔐 Secrets Strategy

Vault stores sensitive credentials for internal services:
- Vaultwarden SMTP credentials
- Traefik dashboard credentials
- Future webhook/API tokens

Initially secrets are manually populated. Future integration will use:
- Vault Agent
- Template-based `.env` injection

---

## 🛡️ Security Notes

- Vault is initialized and unsealed manually on startup (automated unseal TBD)
- Future: mTLS enforcement and Vault Agent auto-auth (AppRole)
