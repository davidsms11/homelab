# Network

## Overview

The Home Lab uses a simple flat network connected through a Telstra router.

The environment is designed to provide secure local access while supporting remote connectivity through Tailscale.

---

## Topology

```text
Internet
    │
    ▼
Telstra Router
    │
    ▼
Proxmox VE
    │
    ├── Debian 13 VM
    │      ├── Docker
    │      │      ├── Homepage
    │      │      ├── Portainer
    │      │      ├── Jellyfin
    │      │      └── Nextcloud
    │      │
    │      ├── Samba
    │      └── Tailscale
    │
    └── Pi-hole (Planned)
```

---

## Components

| Component      | Description             |
| -------------- | ----------------------- |
| Internet       | External connectivity   |
| Telstra Router | Default gateway         |
| Proxmox VE     | Hypervisor              |
| Debian 13 VM   | Main application server |
| Docker         | Container platform      |
| Samba          | Local file sharing      |
| Tailscale      | Secure remote access    |

---

## Services

| Service   | Access     |
| --------- | ---------- |
| Homepage  | Local      |
| Portainer | Local      |
| Jellyfin  | Local      |
| Nextcloud | Local      |
| Samba     | SMB        |
| Tailscale | Remote VPN |

---

## Planned Improvements

* Configure Reverse Proxy
* Enable HTTPS
* Implement VLANs
* Improve firewall configuration
* Add network monitoring
