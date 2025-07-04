# Monitoring Strategy

## 🎯 Current State

| Component         | Monitoring Tool   | Status       | Notes                                           |
|-------------------|-------------------|--------------|-------------------------------------------------|
| `ruby-z04-node-s01` | None active       | Planned      | Will add basic metrics collection (CPU, disk)   |
| Docker Services    | None active       | Planned      | Intend to add service health visibility         |
| HAOS VM            | Not yet deployed  | Planned      | Monitoring plan TBD after VM provisioning       |

---

## 🔭 Confirmed Plans

- Use lightweight agent (e.g., Prometheus Node Exporter) on `ruby-z04-node-s01`
- Explore container-level monitoring after VM and volume strategy are finalized
- Create local dashboard or integrate into Grafana (pending deployment)

---

## 📌 Observability Targets

| Metric Type        | Source                  | Priority   |
|--------------------|--------------------------|------------|
| Node CPU/RAM       | Host (Node Exporter)     | High       |
| Disk usage         | `/opt/data`, `/opt/vm/`  | High       |
| Container uptime   | Docker                   | Medium     |
| HAOS reachability  | VM status + ping         | High       |

---

## 🧪 Future Work

- [ ] Deploy Node Exporter or alternative lightweight agent
- [ ] Evaluate Docker monitoring tools (e.g., cAdvisor, Prometheus config)
- [ ] Create `/automation/alerting.md` when thresholds are defined
- [ ] Determine alerting thresholds for service health (e.g., Traefik down, Vault unsealed)


---

## Planned Tools

- **Node Exporter**: Collect host-level metrics (CPU, disk, memory)
- **Prometheus**: Optional future pull-based aggregation
- **Netdata**: Considered but not yet deployed

---

## Status

- Monitoring stack not yet deployed
- Will be hosted on `ruby-z04-node-s01` once baseline services are stabilized
