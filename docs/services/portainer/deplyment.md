# Portainer Installation

## Objective

Deploy Portainer Community Edition to manage Docker containers through a web interface.

---

## Create the Persistent Volume

Create a Docker volume to store the Portainer configuration.

```bash
docker volume create portainer_data
```

---

## Deploy the Container

```bash
docker run -d \
  -p 8000:8000 \
  -p 9443:9443 \
  --name portainer \
  --restart=always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  portainer/portainer-ce:lts
```

---

## Verification

Verify that the container is running:

```bash
docker ps
```

View the container logs:

```bash
docker logs portainer
```

---

## Container Management

Restart the container:

```bash
docker restart portainer
```

Stop the container:

```bash
docker stop portainer
```

Start the container:

```bash
docker start portainer
```

---

## Password Recovery

Reset the administrator password:

```bash
docker run --rm \
  -v portainer_data:/data \
  portainer/helper-reset-password
```

---

## Notes

* Portainer is deployed using the official Community Edition image.
* Configuration data is stored in the `portainer_data` Docker volume.
* The Docker socket is mounted to allow Portainer to manage local Docker containers.
* The container is configured to restart automatically after system reboots.
