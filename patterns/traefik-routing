# Pattern: Traefik Routing and Exposure Strategy

## Summary

This pattern defines how services in the homelab are exposed via the Traefik reverse proxy running on `ruby-z04-node-s01`.

Traefik is used to route both **LAN-only traffic** and selected **public-facing services**, such as Vaultwarden, using domain-based routing, Docker labels, and optional security middleware.

---

## 🧩 Design Highlights

- **Deployment Mode**: Docker container with Compose
- **Networking**: Connected to custom bridge `br0`
- **Routing Mechanism**: Docker labels per container
- **Certificate Strategy**: Let's Encrypt (or self-signed, internal CA)
- **Security Layers**:
  - Basic Auth (middleware)
  - HTTPS enforced on all routes
  - Public services require explicit opt-in

---

## 🌍 Exposure Policy

| Traffic Scope     | Routing Strategy                     |
|-------------------|--------------------------------------|
| LAN-only services | `.local` domains, private routers    |
| Internet-facing   | Public subdomains (e.g., `vault.rutabagel.com`) with TLS and auth |
| Blocked           | No route or explicitly denied        |

---

## 🏷️ Routing Label Template (Docker Compose)

```yaml
labels:
  - "traefik.enable=true"
  - "traefik.http.routers.vaultwarden.rule=Host(`vault.rutabagel.com`)"
  - "traefik.http.routers.vaultwarden.entrypoints=websecure"
  - "traefik.http.routers.vaultwarden.tls=true"
  - "traefik.http.routers.vaultwarden.middlewares=auth@file"
```

---

## 🔐 Basic Auth Middleware Template (`dynamic_config.toml`)

```toml
[http.middlewares.auth.basicAuth]
users = [
  "admin:$apr1$abc123$EXAMPLEHASH"
]
```

---

## 🔄 Common Use Cases

| Service         | Access        | Method                     |
|-----------------|---------------|----------------------------|
| Vaultwarden     | Public HTTPS  | Subdomain + auth           |
| Home Assistant  | LAN-only      | Internal DNS only          |
| UniFi Controller| LAN-only      | Internal + static IP route |

---

## 📝 Notes

- Middleware is defined in a separate dynamic config file loaded by Traefik.
- Public services must be intentionally configured — default is no public exposure.
- Subdomains should resolve via public DNS (e.g., Cloudflare, Namecheap).
