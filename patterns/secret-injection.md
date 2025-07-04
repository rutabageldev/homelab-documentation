# Pattern: Vault Secret Injection via Template Agent

## Summary

Future services will retrieve secrets at runtime using **Vault Agent with template rendering**.

Secrets will be mounted into containers as plain files, environment files, or individual values — replacing static `.env` files.

---

## Structure

```hcl
# vault-agent-config.hcl
auto_auth {
  method "approle" {
    mount_path = "auth/approle"
    config = {
      role_id_file_path = "/etc/vault/role_id"
      secret_id_file_path = "/etc/vault/secret_id"
    }
  }
}

template {
  source      = "/etc/vault/templates/env.tpl"
  destination = "/secrets/.env"
}
```

---

## Compose Integration

```yaml
volumes:
  - /opt/secrets/vaultwarden.env:/secrets/.env:ro
env_file:
  - /secrets/.env
```

---

## Example Template File

```hcl
SMTP_USERNAME={{ with secret "kv/data/vaultwarden" }}{{ .Data.data.username }}{{ end }}
SMTP_PASSWORD={{ with secret "kv/data/vaultwarden" }}{{ .Data.data.password }}{{ end }}
```

---

## Benefits

- Eliminates plaintext `.env` files under version control
- Enables dynamic secret rotation
- Centralizes auditing and access control

---

## Considerations

- Vault must be running and unsealed before containers can start
- Requires attention to race conditions and service restart logic
- File permissions and injection paths must be tightly controlled
