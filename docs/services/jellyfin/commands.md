# Jellyfin Commands

## Deployment

Start the service:

```bash
docker compose up -d
```

Stop the service:

```bash
docker compose stop
```

Start existing containers:

```bash
docker compose start
```

Restart the container:

```bash
docker restart jellyfin
```

---

## Status

List running containers:

```bash
docker ps
```

Check the Compose status:

```bash
docker compose ps
```

Inspect the container:

```bash
docker inspect jellyfin
```

---

## Logs

View the logs:

```bash
docker logs jellyfin
```

View the last 50 log lines:

```bash
docker logs --tail 50 jellyfin
```

---

## Access the Container

Open a shell inside the container:

```bash
docker exec -it jellyfin bash
```

Exit the shell:

```bash
exit
```

---

## Storage Verification

Verify that the host can see the media files:

```bash
find /mnt/<storage-name>/media -type f | head -20
```

Verify that Jellyfin can see the same files:

```bash
docker exec jellyfin find /media -type f | head -20
```

List the media directory:

```bash
docker exec jellyfin ls -lah /media
```

---

## Updates

Download the latest image:

```bash
docker compose pull
```

Recreate the container:

```bash
docker compose up -d
```

---

## Troubleshooting

Inspect mounted volumes:

```bash
docker inspect jellyfin
```

Display only the mounted directories:

```bash
docker inspect jellyfin \
  --format '{{range .Mounts}}{{println .Source "->" .Destination}}{{end}}'
```

Check the Jellyfin version:

```bash
docker exec jellyfin jellyfin --version
```
