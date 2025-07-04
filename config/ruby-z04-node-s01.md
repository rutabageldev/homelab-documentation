# ruby-z04-node-s01

## 🧾 Description
General-purpose utility node (Lenovo ThinkCentre M910q) located in Zone 04 (Office).  
This device serves as the primary host for utility services, to include infrastructure, in the homelab.  

## 🛠️ Hardware
- Model: Lenovo ThinkCentre M910q Tiny
- CPU: Intel i5-7500T @ 2.7GHz
- RAM: 16GB DDR4
- Storage: 256GB NVMe SSD
- Networking: Ethernet (hardwired to core switch)

## 💻 Operating System
- OS: Ubuntu 22.04 LTS (headless)
- Kernel: [redacted]
- Hostname: `ruby-z04-node-s01.local`
- Static IP: `{{NODE_S01_IP}}` (DHCP reservation via pfSense)
- VLAN: RubyRoot (VLAN 1)

## 🧱 Role
This node acts as the primary infrastructure server and is currently responsible for:
- Hosting key containerized services via Docker
- Acting as the interface between smart home, local services, and internal orchestration
- Running persistent background services and scheduled jobs

## 🐳 Docker Runtime
- Engine: Docker CE (installed via convenience script)
- Compose: Docker Compose v2
- Networking:
  - Default bridge disabled
  - Custom bridge `br0` with host IP passthrough
  - Selective use of host networking (e.g., Vault)

For full Docker configuration, see [docker/ruby-z04-node-s01.md](../docker/ruby-z04-node-s01.md)

## 📦 Hosted Applications
| Service         | Description                          | Docs                                         |
|------------------|--------------------------------------|----------------------------------------------|
| Home Assistant   | Smart home automation platform       | [home-assistant](../apps/home-assistant.md)  |
| Vault            | Secrets management (HashiCorp Vault) | [vault](../apps/vault.md)                    |
| Vaultwarden      | Bitwarden-compatible password vault  | [vaultwarden](../apps/vaultwarden.md)        |
| Traefik          | Reverse proxy & service router       | [traefik](../apps/traefik.md)                |

## 🔐 Access & Security
- SSH access restricted to trusted clients
- Node is not exposed externally (LAN-only access)
- Services secured via basic auth, mTLS (future), or Vault-seeded secrets

## 📋 Future Enhancements
- Add monitoring agent (e.g., Prometheus node exporter)
- Schedule daily backups of service volumes
- Add external SSD for expanded persistent storage
- Replace static secrets with Vault Agent injection
