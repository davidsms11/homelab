# Homepage

## Overview

Homepage is the main dashboard of the Home Lab.

It provides a single interface for accessing self-hosted services, monitoring their availability and organizing links to applications running in the environment.

---

## Purpose

Homepage is used to:

* Centralize access to services
* Organize applications by category
* Display service status
* Simplify administration
* Provide a clean landing page

---

## Features

Current dashboard includes shortcuts for:

* Portainer
* Jellyfin
* Nextcloud

Additional services will be added as the Home Lab grows.

---

## Deployment

Homepage is deployed as a Docker container.

Container data is stored on persistent storage outside the container filesystem.

Deployment details are documented in:

* `deployment.md`

---
