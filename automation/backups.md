# Backup Strategy

## 🗂️ Confirmed Storage Strategy

| Target              | Backup Status     | Notes                                                             |
|---------------------|-------------------|-------------------------------------------------------------------|
| Home Assistant (HA) | Planned           | Will back up HAOS VM image and/or config via snapshots or export |
| Vaultwarden         | Planned           | Plan to back up service volume or bind mount                     |
| Vault               | Not yet defined   | Backups not yet configured; secrets stored in container          |
| Docker Volumes      | Manual snapshot   | Manual backups prior to container teardown                       |

---

## 🧠 Node-Level Backups

- No automated system-level snapshots or image backups are active.
- External SSD planned for `/opt/data` volume expansion and backup mount.
- File-based backups or rsync strategy to be determined.

---

## 📅 Confirmed Plans

- [ ] Schedule daily backups of service volumes (Vaultwarden, Vault, etc.)
- [ ] Explore mounting `/opt/backups` from external SSD
- [ ] Add backup logic to `crontab` or systemd timer
- [ ] Document `restore.md` workflow once backup process is proven

---

## 🧪 Example Backup Targets (Planned)

| Service        | Method                      | Target Path               |
|----------------|-----------------------------|---------------------------|
| HAOS VM        | Libvirt VM snapshot/export  | `/opt/vm/`                |
| Vaultwarden    | Docker volume sync          | `/opt/docker/vaultwarden`|
| Vault          | TBD (Vault CLI/export)      | `/opt/docker/vault`      |

---

## ⚠️ Gaps to Address

- No remote or offsite backups planned yet
- Vault backups must consider encryption and credential protection
