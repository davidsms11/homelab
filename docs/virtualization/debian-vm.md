# Debian 13 Virtual Machine

## Overview

A Debian 13 virtual machine is used as the primary application server for the Home Lab.

The VM hosts Docker and all self-hosted services while Proxmox is responsible only for virtualization.

---

## Virtual Machine Configuration

| Resource         | Value      |
| ---------------- | ---------- |
| Operating System | Debian 13  |
| Memory           | 4 GB       |
| Virtual Disk     | 50 GB      |
| Platform         | Proxmox VE |

---

## Initial Setup

After installing Debian, the following tasks were completed:

* Updated the operating system.
* Installed the `sudo` package.
* Added the primary user to the `sudo` group.
* Verified network connectivity.
* Prepared the system for Docker.

---

## Commands Used

Update package lists:

```bash
sudo apt update
```

Upgrade installed packages:

```bash
sudo apt full-upgrade -y
```

Install sudo (using the root account):

```bash
su -
apt install sudo
```

Add the primary user to the sudo group:

```bash
usermod -aG sudo <username>
```

Verify the current user:

```bash
whoami
```

Verify the operating system:

```bash
cat /etc/os-release
```

Verify disk usage:

```bash
df -h
```

Verify memory usage:

```bash
free -h
```

---

## Troubleshooting

### sudo: command not found

The default Debian installation did not include the `sudo` package.

The issue was resolved by logging in as the root user, installing the package and adding the primary user to the `sudo` group.

---

## Next Step

After the initial configuration, the system was prepared for Docker installation and deployment of self-hosted services.
