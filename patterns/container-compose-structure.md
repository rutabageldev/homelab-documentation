# Pattern: Container Directory and Compose Structure

## Summary

Each service is defined and managed in its own self-contained directory under:

```
/opt/services/<service-name>/
```

### Directory Layout

```
/opt/
├── services/
│   ├── traefik/
│   │   ├── docker-compose.yml
│   │   └── config/
│   ├── vaultwarden/
│   │   ├── docker-compose.yml
│   └── vault/
```

Volumes are mounted under:

```
/opt/data/<service-name>/
```

### Benefits

- Keeps runtime, config, and orchestration logic co-located
- Supports backups and portability at the service level
- Works with `docker-compose@<service>.service` systemd units

### Example systemd unit

```ini
[Unit]
Description=Docker Compose App - %i
Requires=docker.service
After=docker.service

[Service]
Type=oneshot
RemainAfterExit=yes
WorkingDirectory=/opt/services/%i
ExecStart=/usr/bin/docker compose up -d
ExecStop=/usr/bin/docker compose down

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl enable --now docker-compose@vaultwarden.service
```
