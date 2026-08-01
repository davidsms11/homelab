# Virtualization

## Overview

The Home Lab uses Proxmox VE as the virtualization platform.

A single Debian 13 virtual machine hosts all Docker services, while Proxmox is responsible only for managing the infrastructure.

---

## Hypervisor

| Component    | Value               |
| ------------ | ------------------- |
| Platform     | Proxmox VE          |
| Installation | Bare Metal          |
| Host         | HP EliteDesk 800 G3 |

---

## Virtual Machines

| VM     | Operating System | Purpose                            |
| ------ | ---------------- | ---------------------------------- |
| Debian | Debian 13        | Docker host and application server |

---

## Current Architecture

```text
HP EliteDesk 800 G3
        │
        ▼
   Proxmox VE
        │
        ▼
   Debian 13 VM
        │
        ├── Docker
        ├── Samba
        └── Tailscale
```

---

## Design Decisions

The virtualization layer is kept separate from application services.

Proxmox manages the infrastructure, while all applications are deployed inside the Debian virtual machine. This simplifies maintenance, backups and future migration to different hardware.

---

## Related Documentation

- [Proxmox Installation](/docs/virtualization/proxmox-install.md)
- [Debian VM Setup](/docs/virtualization/debian-vm.md)
