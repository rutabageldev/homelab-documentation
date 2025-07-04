# ADR-001: Container Orchestration on Utility Node

**Status**: Accepted  
**Date**: 2025-06-22  
**Context**: ruby-z04-node-s01 (Lenovo ThinkCentre M910q)

## Decision

We replaced a bare-metal Home Assistant OS installation with a headless Ubuntu 22.04 LTS environment to serve as a general-purpose container host.

This enables the node to run:
- Reverse proxy and ingress (Traefik)
- Secrets management (Vault)
- Password manager backend (Vaultwarden)
- Local services like Home Assistant (to be re-deployed in a VM)

Container orchestration is managed via Docker Compose v2, with optional systemd integration for service persistence and restart on boot.

## Rationale

- Provides flexibility to run a broader set of utility services
- Allows finer control over container lifecycle, orchestration, and networking
- Enables future VM-based HAOS re-deployment with host-level access to other containers

## Consequences

- Requires additional setup and maintenance for system updates, network bridges, and backups
- HAOS must now run in a VM instead of directly on hardware
