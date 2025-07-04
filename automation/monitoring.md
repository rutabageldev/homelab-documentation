# Automation: Monitoring

## Goals

- Lightweight monitoring of system state and service health
- Local-first monitoring (no cloud dependencies)

---

## Planned Tools

- **Node Exporter**: Collect host-level metrics (CPU, disk, memory)
- **Prometheus**: Optional future pull-based aggregation
- **Netdata**: Considered but not yet deployed

---

## Status

- Monitoring stack not yet deployed
- Will be hosted on `ruby-z04-node-s01` once baseline services are stabilized

---

## Future Steps

- Add monitoring as part of post-HAOS VM stabilization
- Determine alerting thresholds for service health (e.g., Traefik down, Vault unsealed)
