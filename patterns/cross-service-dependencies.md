# Pattern: Cross-Service Dependencies

## 🧬 Service Coupling Overview

Documented dependencies between core services hosted on `ruby-z04-node-s01`.

---

## 📦 Confirmed Dependencies

| Service        | Depends On           | Notes                                                             |
|----------------|----------------------|-------------------------------------------------------------------|
| Vaultwarden    | Traefik              | Routed internally via `vault.rutabagel.com` through Traefik       |
| Vaultwarden    | Vault (planned)      | Plan to inject secrets via Vault Agent                            |
| Home Assistant | Traefik              | Was proxied via Traefik before teardown; will be again post-VM    |
| HAOS VM        | `br0` bridge         | Must be bound to bridged network interface (`br0`) on startup     |

---

## 🛠️ Startup Requirements

- The custom bridge `br0` must be brought up via `force-br0-up.service` systemd unit  
- Vault must be available before dependent services (e.g., Vaultwarden, Traefik with Vault configs)  
- HAOS VM relies on bridge to bind network interfaces

No specific use of `depends_on` or orchestration sequencing currently exists.
