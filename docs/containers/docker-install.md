# Docker Installation

## Objective

Install Docker Engine on the Debian virtual machine used by the Home Lab.

---

## Requirements

* Debian 13 virtual machine
* Internet connection
* User with `sudo` privileges

---

## Update the System

```bash
sudo apt update
sudo apt full-upgrade -y
```

---

## Install Docker

```bash
sudo apt install docker.io -y
```

---

## Enable Docker

Enable the Docker service to start automatically at boot.

```bash
sudo systemctl enable docker
```

Start the Docker service.

```bash
sudo systemctl start docker
```

---

## Verification

Check the installed Docker version.

```bash
docker --version
```

Verify that the Docker service is running.

```bash
sudo systemctl status docker
```

List running containers.

```bash
docker ps
```

List all containers.

```bash
docker ps -a
```

---

## Basic Test

Run a simple container to verify that Docker is working correctly.

```bash
sudo docker run hello-world
```

---

## Result

Docker Engine is installed and ready to deploy containerized applications.

The next step is to install and configure Docker Compose before deploying services.

---


References

Official Docker Documentation

https://docs.docker.com/engine/install/debian/