# ADR-003: Secrets Management via Vault

**Status**: Accepted  
**Date**: 2025-06-29  
**Context**: ruby-z04-node-s01 and dependent containers

---

## Decision

We will centralize secrets management using **HashiCorp Vault**, running as a container on `ruby-z04-node-s01` in `host` networking mode.

The initial goal is to store static secrets for:
- Vaultwarden (SMTP credentials)
- Traefik (basic auth, future mTLS support)
- Future services (API tokens, webhook secrets)

In the near term, secrets may be read manually or injected via `.env` files. The longer-term plan is to use **Vault Agent with template injection** to mount secrets at runtime.

---

## Rationale

- Reduces reliance on plaintext `.env` files scattered across Compose directories
- Enables rotation and auditing of secrets
- Prepares the environment for more secure container services

---

## Consequences

- Vault must be highly available and always running to serve secrets
- Vault Agent integration will require changes to some Compose files or systemd units
- Secrets-injection behavior must be carefully coordinated to avoid race conditions or mount issues during container startup

---

## References

- See service config: [`apps/vault.md`](../apps/vault.md)
- See injection pattern: [`patterns/vault-secret-injection-template.md`](../patterns/vault-secret-injection-template.md)
