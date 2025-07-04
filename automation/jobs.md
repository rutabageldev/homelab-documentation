# Automation: Jobs and Scheduled Tasks

## 🔁 Runtime Management

Service health and reliability is reinforced with job-level automation via `systemd` and `cron`.

---

## 📆 Job Categories

| Job Type         | Tool     | Description                                  |
|------------------|----------|----------------------------------------------|
| Backups          | `cron`   | rsync data volumes to external storage       |
| HAOS VM control  | `systemd`| Start VM on boot, optionally snapshot daily  |
| Docker pruning   | `cron`   | Weekly container/image cleanup               |
| Log rotation     | `logrotate`| Trim large service logs from bind mounts |

---

## 🧠 Sample: Daily Backup Job

```cron
0 3 * * * /usr/local/bin/backup-docker-volumes.sh
```

```bash
#!/bin/bash
SRC="/opt/data/"
DEST="/mnt/backup-node/"
rsync -av --delete "$SRC" "$DEST"
```

Add to:
```bash
crontab -e
```

---

## 🖥️ HAOS Snapshot Planning

Planned pattern:

- Use `virsh` commands to snapshot VM before nightly backup
- Optionally export snapshot to external volume

```bash
virsh snapshot-create-as haos-vm pre-backup --disk-only --atomic
```

---

## 🔄 HAOS Restart Logic

Option to schedule restart for stability:
```cron
0 5 * * 0 /usr/bin/virsh reboot haos-vm
```

---

## 🔧 Future Enhancements

- Replace cron with `systemd` timers for tighter dependency control
- Tag backup runs with timestamps
- Use `logger` to report job status to syslog
