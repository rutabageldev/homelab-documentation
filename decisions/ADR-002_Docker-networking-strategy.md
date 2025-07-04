# ADR-002: Docker Networking Strategy

**Status**: Accepted  
**Date**: 2025-06-23  
**Context**: ruby-z04-node-s01

## Decision

We disabled Docker's default bridge and implemented a manually configured `br0` Linux bridge with host passthrough. Containers can use:

- `br0`: for static IP assignment via DHCP reservations (pfSense)
- `host`: for raw port exposure when required (e.g., Vault)

Additional named Docker bridges (e.g., `homelab_lan`) may be defined for specific inter-container use cases.

## Rationale

- Enables clean IP management across VLANs and physical infrastructure
- Ensures containers receive predictable addresses without Docker NAT
- Allows selectively exposing services to the LAN (but not WAN)

## Consequences

- Requires systemd-based bridge bring-up on boot (`force-br0-up.service`)
- Some containers may need explicit network config for compatibility
- Host-based firewalling is still required for security
