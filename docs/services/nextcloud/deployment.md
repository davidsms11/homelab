# Nextcloud Deployment

## Platform

| Component          | Configuration    |
| ------------------ | ---------------- |
| Container platform | Docker Compose   |
| Application        | Nextcloud        |
| Database           | MariaDB 11       |
| Host system        | Debian 13 VM     |
| Restart policy     | `unless-stopped` |

## Architecture

```text
Docker Compose
├── nextcloud
│   └── Persistent data on dedicated HDD
└── nextcloud-db
    └── Docker named volume
```

## Compose Configuration

The public example below uses placeholders instead of real passwords and storage paths.

```yaml
services:
  db:
    image: mariadb:11
    container_name: nextcloud-db
    restart: unless-stopped
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW

    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: nextcloud
      MYSQL_USER: nextcloud
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}

    volumes:
      - db:/var/lib/mysql

  nextcloud:
    image: nextcloud
    container_name: nextcloud
    restart: unless-stopped

    ports:
      - "<host-port>:80"

    depends_on:
      - db

    environment:
      MYSQL_DATABASE: nextcloud
      MYSQL_USER: nextcloud
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
      MYSQL_HOST: db

    volumes:
      - /mnt/<storage-name>/data:/var/www/html

volumes:
  db:
```

## Storage

Nextcloud application files and user data are stored on a dedicated HDD using a bind mount:

```text
/mnt/<storage-name>/data → /var/www/html
```

MariaDB data is stored in the Docker named volume:

```text
db → /var/lib/mysql
```


## Verification

Check the containers:

```bash
docker compose ps
```

View Nextcloud logs:

```bash
docker compose logs nextcloud
```

View MariaDB logs:

```bash
docker compose logs db
```

Check the Nextcloud bind mount:

```bash
docker inspect nextcloud \
  --format '{{range .Mounts}}{{println .Source "->" .Destination}}{{end}}'
```

Check the database volume:

```bash
docker volume inspect <project-name>_db
```

## Updates

Run from the directory containing the Compose file:

```bash
docker compose pull
docker compose up -d
```

Verify after updating:

```bash
docker compose ps
```

## Backup

A complete backup should include:

* Nextcloud bind-mounted directory
* MariaDB database
* Compose configuration


