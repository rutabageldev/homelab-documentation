# ADR-004: Home Assistant OS Migration to VM

**Status**: Accepted  
**Date**: 2025-06-22  
**Context**: ruby-z04-node-s01

---

## Decision

We decided to decommission the original **bare-metal HAOS installation** and redeploy Home Assistant OS as a **virtual machine** hosted on `ruby-z04-node-s01`.

The VM will be managed using `virt-manager` or `virsh`, with its own bridged network connection to integrate cleanly with the homelab and smart home devices.

---

## Rationale

- The bare-metal install made it difficult to host other services on the node
- A VM allows clean separation of HAOS from other Docker-hosted utilities
- Retains access to full HAOS features (Supervisor, Add-ons, etc.)
- Maintains compatibility with Z-Wave/Zigbee dongles via USB passthrough

---

## Consequences

- Requires additional storage allocation (approx. 32–64 GB for HAOS)
- VM networking must be configured (e.g., bridged to `br0`)
- HA backups and snapshots must now be handled via the VM layer or HA add-ons

---

## References

- Target runtime node: [`config/ruby-z04-node-s01.md`](../config/ruby-z04-node-s01.md)
- VM host strategy: [TBD, under `/vm/` or `/patterns/virtualization/`]
