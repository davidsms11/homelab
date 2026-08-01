# Homepage Deployment

## Objective

Deploy Homepage as the main dashboard for accessing self-hosted services in the Home Lab.

---

## Platform

| Component            | Value                     |
| -------------------- | ------------------------- |
| Platform             | Docker                    |
| Host                 | Debian 13 Virtual Machine |
| Container Management | Docker Compose            |

---

## Deployment

Homepage is deployed using Docker Compose.

Persistent data is stored outside the container to simplify upgrades and backups.

Example volume mapping:

```yaml
services:
  homepage:
    volumes:
      - /mnt/<storage-name>/homepage:/app/config
```

The storage path shown above is an example and does not reflect the actual Home Lab configuration.

---

## Verification

Check that the container is running:

```bash
docker ps
```

View the container logs:

```bash
docker logs <container-name>
```

Verify the Docker Compose configuration:

```bash
docker compose config
```

---

## Updates

Update the Homepage image:

```bash
docker compose pull
```

Recreate the container:

```bash
docker compose up -d
```

---

## Backup

The Homepage configuration is stored in a persistent directory outside the container.

Backing up this directory preserves the dashboard configuration after container recreation.

---

