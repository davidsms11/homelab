# Docker Compose

## Objective

Install Docker Compose on the Debian virtual machine and verify that Compose applications can be deployed successfully.

---

## Requirements

* Debian 13 virtual machine
* Docker Engine installed
* Internet connection
* User with `sudo` privileges

---

## Installation

Update the package index:

```bash
sudo apt update
```

Install Docker Compose:

```bash
sudo apt install docker-compose -y
```

---

## Verification

Check the installed version:

```bash
docker compose version
```

The modern Compose syntax uses a space:

```bash
docker compose
```

Avoid using the legacy command unless it is required by an older installation:

```bash
docker-compose
```

---

## Test Directory

Create a temporary directory:

```bash
mkdir -p ~/compose-test
cd ~/compose-test
```

---

## Test Compose File

Create a file named:

```text
compose.yaml
```

Example:

```yaml
services:
  web:
    image: nginx:alpine
    container_name: compose-test
    ports:
      - "8080:80"
    restart: unless-stopped
```

This is a generic example and does not expose the real Home Lab configuration.

---

## Validate the Configuration

```bash
docker compose config
```

This command checks the Compose file and displays the resolved configuration.

---

## Start the Container

```bash
docker compose up -d
```

---

## Verification

Check the Compose services:

```bash
docker compose ps
```

Check running containers:

```bash
docker ps
```

View container logs:

```bash
docker compose logs
```

---

## Stop and Remove the Test

```bash
docker compose down
```

Remove the test directory:

```bash
cd ~
rm -rf ~/compose-test
```

---

## Common Commands

Start services:

```bash
docker compose up -d
```

Stop services without removing them:

```bash
docker compose stop
```

Start stopped services:

```bash
docker compose start
```

Restart services:

```bash
docker compose restart
```

View service status:

```bash
docker compose ps
```

View logs:

```bash
docker compose logs
```

Follow logs in real time:

```bash
docker compose logs -f
```

Pull updated images:

```bash
docker compose pull
```

Recreate services with updated images:

```bash
docker compose up -d
```

Stop and remove containers and networks:

```bash
docker compose down
```

---

## Security

Public Compose examples must not contain:

* Real usernames
* Internal IP addresses
* Passwords
* API keys
* Access tokens
* Private domains
* Personal directory names
* Real `.env` files

Sensitive values should be stored in an `.env` file that is excluded from Git.

Example:

```yaml
services:
  application:
    environment:
      APP_USER: ${APP_USER}
      APP_PASSWORD: ${APP_PASSWORD}
```

Example `.env.example`:

```text
APP_USER=<username>
APP_PASSWORD=<replace-with-secure-password>
```

The real `.env` file must not be committed.

---

## Related Documentation

* [Containers Overview](README.md)
* [Docker Installation](docker-install.md)
* [Storage](../storage/README.md)
