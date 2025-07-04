# 🏠 Homelab Documentation

This repository contains documentation, inventories, and reference materials for my personal homelab environment and related tools.

It’s intended to track physical hardware, portable kits, container orchestration, service-level configuration, and recovery utilities in a clear, version-controlled format.

---

## 📁 Contents

| Folder           | Purpose                                                                 |
|------------------|-------------------------------------------------------------------------|
| `config/`        | Node-level configuration and role descriptions for physical devices     |
| `docker/`        | Docker runtime and orchestration details for each node                  |
| `apps/`          | Application-specific configuration and behavior (e.g., Vault, Traefik)  |
| `automation/`    | Patterns for backups, CI/CD, logging, and monitoring                    |
| `decisions/`     | Key architectural and infrastructure decisions using the ADR format     |
| `patterns/`      | Reusable orchestration patterns for containers, secrets, and routing    |
| `jobs/`          | Examples of active or archived jobs/automation records                  |
| `ledgerly/`      | Subproject-specific infrastructure and data model planning              |
| [`jump-kit-inventory.md`](./jump-kit-inventory.md) | Inventory of portable kit for diagnostics and recovery              |
| `changelog.md`   | Tracks notable changes to the homelab's infrastructure or services      |

---

## 🧠 Goals

- Maintain accurate, lightweight documentation for homelab operations
- Track portable hardware and utilities for remote development and diagnostics
- Document repeatable processes (e.g., OS installs, firmware updates, and jump box use)
- Version and evolve kits, services, and infrastructure over time

---

## 🧱 Current Focus

- Docker-based service orchestration with Vault, Traefik, and Vaultwarden
- HAOS re-deployment in a VM with persistent volume support
- Secrets management via Vault with future Vault Agent injection
- Consistent volume mount, network bridge, and reverse proxy patterns

---

## 🚧 In Progress

- HAOS via libvirt VM
- Vault mTLS and secret injection workflows
- Monitoring agent integration (e.g., Node Exporter)
- External storage (e.g., `/opt/data`) and backup jobs
- Roadmap + dependency visualization

---

## 🔐 Networking & Security Principles

- Static DHCP reservations via pfSense
- Services run on LAN-only unless explicitly exposed (e.g., Vaultwarden via Traefik)
- Selective use of host networking (e.g., Vault)
- Reverse proxy via Traefik with subdomain routing and DNS integration

---

## 🔖 Related Docs

- [device-naming.yaml](./device-naming.yaml) — Structured naming convention
- [changelog.md](./changelog.md) — Operational evolution
- [patterns/](./patterns/) — Canonical infrastructure behaviors
- [decisions/](./decisions/) — Architectural decisions (ADRs)

---

## ✅ Principles

- Modular, auditable configurations
- Explicit design over implicit convention
- Internal consistency across hardware, orchestration, and services
- Repeatable setup and recovery flows
