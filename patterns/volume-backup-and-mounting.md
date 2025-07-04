# Pattern: Volume Mounting and Backup Strategy

## Summary

All persistent data for containerized services is stored under:

```
/opt/data/<service-name>/
```

This enables:
- Clear mapping of container mounts
- Easy rsync- or restic-based backups
- Future move to external SSD for expanded storage

---

## Mounting Strategy

- Use **bind mounts** (not named volumes) for full host control
- Mounts are defined per service in their respective Compose files:

```yaml
volumes:
  - /opt/data/vaultwarden/:/data/
```

- Secrets may also be injected as bind-mounted files using Vault Agent templates in the future

---

## Backup Targets

| Directory             | Contents                     |
|------------------------|------------------------------|
| `/opt/data/vaultwarden/` | DB, config.json             |
| `/opt/data/traefik/`      | Dynamic config, certs       |
| `/opt/data/vault/`        | Vault storage backend       |

---

## Backup Method

- TBD: likely `rsync` to NAS or external SSD
- Optional integration with snapshot tools (`zfs`, `btrfs`, or filesystem-level snapshots)

---

## Notes

- Consider using `--read-only` flags or filesystem protections for mounted secrets
- Align backup cadence with service criticality
