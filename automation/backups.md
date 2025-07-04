# Automation: Backups

## Strategy

Backups focus on Docker bind-mounted volumes under `/opt/data/`, which host persistent state for:

- Vaultwarden
- Vault
- Traefik
- Future services (e.g., Gitea, N8N)

---

## Targets

| Path                     | Notes                        |
|--------------------------|------------------------------|
| `/opt/data/vaultwarden/` | Vault + config.json          |
| `/opt/data/vault/`       | Storage backend (filesystem) |
| `/opt/data/traefik/`     | Dynamic config, certs        |

---

## Methods

- Initial backup method: `rsync` to external SSD or NAS
- Long-term goal: use `restic` or `borg` with scheduling
- Potential integration with `systemd` timers or `cron`

---

## Next Steps

- Set up `daily-backup.service` and `daily-backup.timer`
- Secure destination paths with minimal permissions
