# Pattern: Service Lifecycle and Resilience

## Goal

Ensure key services (Traefik, Vault, HAOS VM) recover cleanly after:

- Node reboot
- Bridge misalignment
- Host-level Docker failure

---

## 🧩 Key Techniques

1. **Bridge pre-flight unit**
   - Ensures `br0` is up before containers or VMs start

2. **Compose-level restart policy**

```yaml
restart: unless-stopped
```

3. **systemd wrapper for critical services**
   - Ensures Vault or Traefik can restart even outside Docker’s scope
   - Can optionally alert or restart Docker engine

4. **Post-failure recovery script** (planned)
   - Monitor logs for panic/stall states
   - Restart affected container or VM

---

## Examples

```bash
docker update --restart unless-stopped traefik
```

Or via Compose:
```yaml
services:
  traefik:
    restart: unless-stopped
```

---

## Future Goals

- Add uptime watchdog scripts
- Integrate with monitoring/alerting once deployed
