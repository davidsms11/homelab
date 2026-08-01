# Proxmox VE Installation

## Objective

Deploy Proxmox VE as the virtualization platform for the Home Lab.

---

## Environment

| Component | Value |
|-----------|-------|
| Server | HP EliteDesk 800 G3 |
| CPU | Intel Core i5-6600 |
| Memory | 16 GB DDR4 |
| System Disk | 256 GB NVMe SSD |

---

## Installation Media

- Official Proxmox VE ISO
- Bootable USB

---

## Installation Summary

The installation was performed directly on the physical server using the Proxmox VE installer.

The operating system was installed on the NVMe SSD and configured as the virtualization host for the Home Lab.

---

## Initial Configuration

After the installation, the following tasks were completed:

- Verified network connectivity
- Accessed the Proxmox web interface
- Updated the operating system
- Created the first Debian virtual machine

---

## Verification

Check the installed version:

```bash
pveversion
```

Verify the hostname:

```bash
hostnamectl
```

Verify the network interfaces:

```bash
ip addr
```

Verify disk usage:

```bash
df -h
```

---

## Next Step

After the hypervisor installation, the Debian 13 virtual machine was created.

See:

- [Debian VM Setup](/docs/virtualization/debian-vm.md)