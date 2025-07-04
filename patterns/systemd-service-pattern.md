# Pattern: systemd Services for Container and VM Orchestration

## Summary

Services critical to homelab infrastructure (e.g., Vault, Traefik, HAOS VM) are managed with custom `systemd` units to ensure:

- Reliable startup order
- Dependency control (e.g., wait for `br0`)
- Restart-on-failure behavior

---

## Example: Custom Bridge Pre-flight

```ini
[Unit]
Description=Ensure br0 is up at boot
Before=multi-user.target

[Service]
Type=oneshot
ExecStart=/usr/sbin/ip link set br0 up
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

Saved as:
```
/etc/systemd/system/force-br0-up.service
```

---

## Example: HAOS VM Startup

```ini
[Unit]
Description=Start Home Assistant VM
After=network-online.target force-br0-up.service
Requires=force-br0-up.service

[Service]
ExecStart=/usr/bin/virsh start haos-vm
ExecStop=/usr/bin/virsh shutdown haos-vm
Restart=always

[Install]
WantedBy=multi-user.target
```

---

## Notes

- Place services in `/etc/systemd/system/`
- Enable with `systemctl enable <unit>`
- Use `Requires=` and `After=` for tight dependency control
