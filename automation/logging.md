# Automation: Logging Strategy

## Local Logging

Services running via Docker log to `journald` or Compose-managed stdout by default. Key practices include:

- Avoiding large `log.json` files
- Using `--log-opt max-size` and `max-file`
- Redirecting critical logs to host syslog (future)

---

## Future Enhancements

- Centralize logs to a syslog-compatible service (e.g., Loki)
- Tag container logs by service name
- Add Promtail sidecars (optional)

---

## Sample Compose Snippet

```yaml
logging:
  driver: "json-file"
  options:
    max-size: "10m"
    max-file: "3"
```
