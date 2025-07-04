# Home Assistant (HAOS)

## 🔧 Overview

Home Assistant OS (HAOS) is being redeployed in a **VM** hosted on `ruby-z04-node-s01`, replacing the previous bare-metal install.

---

## 🧱 Deployment (Planned)

| Parameter            | Value                    |
|---------------------|--------------------------|
| Host Node           | ruby-z04-node-s01        |
| Runtime             | KVM / libvirt VM          |
| Networking          | Bridged (`br0`)          |
| Access              | LAN-only (planned mTLS)  |

---

## 🧠 Use Cases

- Home automation control (Hue, Sonos, Nest)
- Dashboard integration 
- Smart home event routing

---

## 📦 Key Add-ons (Planned)

- Node-RED
- File Editor
- Vault integration for secret injection
- Custom MQTT broker (local)

---

## 🔐 Security

- Access limited to LAN via static IP
- mTLS support planned via Traefik or direct NGINX in front of HAOS
