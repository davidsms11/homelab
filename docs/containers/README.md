# Docker

## Overview

Docker is used to deploy and manage self-hosted applications within the Debian virtual machine.

Running applications as containers provides isolation, portability and simplified maintenance while keeping the host operating system clean.

---

## Architecture

```text
Proxmox VE
        │
        ▼
   Debian 13 VM
        │
        ▼
 Docker Engine
        │
        ├── Homepage
        ├── Portainer
        ├── Nextcloud
        └── Jellyfin
```

---

## Container Management

Containers are managed using Docker and Docker Compose.

Container configuration is stored separately from application data, allowing containers to be recreated without affecting persistent files.

---

## Persistent Storage

Persistent data is stored outside containers using bind mounts.

Example:

```yaml
services:
  application:
    volumes:
      - /mnt/<storage-name>/application-data:/config
```

This approach keeps application data independent from the container lifecycle.

---

## Network

Containers communicate through Docker networking while remaining accessible from the local network when required.

Networking is configured to support communication between services without exposing unnecessary ports.

---

## Verification

Check the Docker version:

```bash
docker --version
```

List running containers:

```bash
docker ps
```

List all containers:

```bash
docker ps -a
```

List Docker images:

```bash
docker image ls
```

List Docker volumes:

```bash
docker volume ls
```

List Docker networks:

```bash
docker network ls
```

---

## Design

Docker was selected because it provides:

* Simple application deployment
* Easy updates
* Service isolation
* Persistent storage support
* Reproducible configurations
* Lightweight virtualization

---

## Related Documentation

* Virtualization
* Storage
* Homepage
* Nextcloud
* Jellyfin
* Samba
