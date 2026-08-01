# Storage

## Overview

The Home Lab uses separate storage for the operating system and application data.

The Proxmox installation and virtual machine disks are stored on the system drive, while a dedicated HDD is used for persistent application data, media files and network shares.

---

## Storage Layout

| Storage             | Purpose                                             |
| ------------------- | --------------------------------------------------- |
| NVMe SSD            | Proxmox VE and virtual machine storage              |
| Data HDD            | Persistent application data, media and shared files |
| Debian virtual disk | Debian operating system and installed packages      |

---

## Mount Point

The data drive is mounted inside the Debian virtual machine using a dedicated mount point.

Example:

```text
/mnt/<storage-name>
```

The real mount path is not published in this repository.

---

## Directory Structure

```text
/mnt/<storage-name>/
├── application-data/
├── media/
│   ├── movies/
│   ├── series/
│   └── videos/
└── shared-files/
```

The directory structure separates application data from media and shared files.

---

## Storage Usage

| Service   | Storage purpose                            |
| --------- | ------------------------------------------ |
| Nextcloud | Persistent user files and application data |
| Jellyfin  | Media library                              |
| Samba     | Local network file sharing                 |
| Docker    | Bind-mounted persistent data               |

---

## Persistent Mounting

The disk is configured to mount automatically when the Debian virtual machine starts.

The configuration is managed through:

```text
/etc/fstab
```

Before changing this file, the disk UUID can be identified using:

```bash
lsblk -f
```

or:

```bash
sudo blkid
```

The mount configuration should use the disk UUID instead of a device name such as `/dev/sdb1`, because device names may change.

Example:

```text
UUID=<disk-uuid> /mnt/<storage-name> ext4 defaults,nofail 0 2
```

Do not publish the real disk UUID in the public repository.

---

## Mount Verification

Verify that the disk is mounted:

```bash
findmnt /mnt/<storage-name>
```

Check available disk space:

```bash
df -h
```

Inspect disks and filesystems:

```bash
lsblk -f
```

List the storage directories:

```bash
ls -la /mnt/<storage-name>
```

---

## Docker Integration

Docker services access persistent storage through bind mounts.

Example:

```yaml
services:
  application:
    volumes:
      - /mnt/<storage-name>/application-data:/config
      - /mnt/<storage-name>/media:/media
```

This keeps important data outside the container filesystem.

Containers can be recreated or updated without deleting persistent files.

---

## File Access Verification

Verify that files are visible on the Debian host:

```bash
find /mnt/<storage-name>/media -type f | head
```

Verify that the same files are visible inside a container:

```bash
docker exec <container-name> find /media -type f | head
```

This helps identify incorrect volume mappings or permission problems.

---

## Permissions

Storage directories must have suitable ownership and permissions for Docker services and Samba.

Inspect permissions:

```bash
ls -ld /mnt/<storage-name>
```

Inspect ownership recursively:

```bash
find /mnt/<storage-name> -maxdepth 2 -printf '%M %u:%g %p\n'
```

Example ownership change:

```bash
sudo chown -R <username>:<groupname> /mnt/<storage-name>
```

---

## Design

Persistent data is stored outside Docker containers so that:

* Containers can be recreated safely.
* Application data remains available after updates.
* Multiple services can access shared directories.
* Backups can target known storage locations.
* Storage problems can be diagnosed from the Debian host.

---

## Security

The public documentation does not include:

* Real disk UUIDs
* Hostnames
* Usernames
* Internal IP addresses
* Private filenames
* Personal directory names
* Complete `/etc/fstab` contents
