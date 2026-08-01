# Jellyfin Deployment

## Objective

Deploy Jellyfin as a self-hosted media server using Docker Compose.

---

## Create the Directories

```bash
mkdir -p ~/jellyfin/config
mkdir -p ~/jellyfin/cache
cd ~/jellyfin
```

---

## Docker Compose Configuration

Create a file named:

```text
docker-compose.yml
```

Example configuration:

```yaml
services:
  jellyfin:
    image: jellyfin/jellyfin
    container_name: jellyfin

    ports:
      - "8096:8096"
      - "7359:7359/udp"

    volumes:
      - ./config:/config
      - ./cache:/cache
      - /mnt/<storage-name>/media:/media

    restart: unless-stopped
```

The real storage path is replaced with a placeholder in the public repository.

---

## Deploy Jellyfin

Run from the directory containing the Compose file:

```bash
docker compose up -d
```

---

## Verification

Check the container status:

```bash
docker compose ps
```

View the logs:

```bash
docker logs jellyfin
```

Verify that the media directory is accessible inside the container:

```bash
docker exec jellyfin ls -lah /media
```

List some media files:

```bash
docker exec jellyfin find /media -type f | head -20
```

---

## Container Management

Restart Jellyfin:

```bash
docker restart jellyfin
```

Stop Jellyfin:

```bash
docker compose stop
```

Start Jellyfin:

```bash
docker compose start
```

---

## Updates

Pull the latest image:

```bash
docker compose pull
```

Recreate the container:

```bash
docker compose up -d
```

Check the service after updating:

```bash
docker compose ps
```

---

## Storage

Jellyfin uses three bind mounts:

| Container path | Purpose                                   |
| -------------- | ----------------------------------------- |
| `/config`      | Jellyfin configuration and database       |
| `/cache`       | Cache and temporary transcoding files     |
| `/media`       | Media library stored on the dedicated HDD |

The configuration and cache directories are located beside the Docker Compose file.

---

## Troubleshooting

Check whether the host can access the media files:

```bash
find /mnt/<storage-name>/media -type f | head
```

Check whether Jellyfin can access the same files:

```bash
docker exec jellyfin find /media -type f | head
```

Inspect the mounted directories:

```bash
docker inspect jellyfin \
  --format '{{range .Mounts}}{{println .Source "->" .Destination}}{{end}}'
```

Review recent logs:

```bash
docker logs jellyfin --tail 50
```

If files exist on the host but not inside the container, verify the volume mapping and directory permissions.

---

## Backup

A Jellyfin backup should include:

* `config/`
* Docker Compose configuration

The cache directory does not normally need to be backed up because Jellyfin can recreate it.

The media library should be included in the separate storage backup process.
