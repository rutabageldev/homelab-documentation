# Application: Traefik Reverse Proxy

## Summary

This document outlines how Traefik is deployed on `ruby-z04-node-s01` to route traffic for containerized services in the homelab.

It handles both internal LAN routing and public ingress for select services (e.g., Vaultwarden), with HTTPS and security middleware enforced.

---

## ⚙️ Deployment Details

- **Location**: `/opt/services/traefik/`
- **Compose File**: `docker-compose.yml`
- **Network Mode**: `br0`
- **Ports Exposed**: `:80`, `:443` (to LAN and optionally WAN)
- **Restart Policy**: `unless-stopped`

---

## 🐳 Compose Configuration (Simplified)

```yaml
version: "3.9"

services:
  traefik:
    image: traefik:v2.11
    container_name: traefik
    restart: unless-stopped
    network_mode: br0
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - /opt/data/traefik/traefik.yml:/etc/traefik/traefik.yml:ro
      - /opt/data/traefik/dynamic/:/etc/traefik/dynamic/
      - /var/run/docker.sock:/var/run/docker.sock
    labels:
      - "traefik.enable=true"
```

---

## 🔐 Security

- Basic Auth middleware defined in `dynamic/auth.toml`
- TLS is enforced via HTTPS-only routes
- Let's Encrypt is supported (pending DNS verification setup)

---

## 📁 Key Files

| File | Purpose |
|------|---------|
| `traefik.yml` | Static config: entryPoints, providers |
| `dynamic/auth.toml` | Middleware: auth, headers |
| `acme.json` | TLS cert storage (encrypted) |
| `docker-compose.yml` | Service definition |
| `traefik.service` (optional) | systemd unit for Traefik container |

---

## 🛠 Maintenance Notes

- Certificates stored in `acme.json` must be permission-restricted (`600`)
- Use `docker logs traefik` or `/logs/traefik.log` for troubleshooting
- Restart with:
  ```bash
  docker compose restart
  ```

---

## 🔗 Related Patterns

- [Traefik Routing Template](/patterns/traefik-routing-template.md)
