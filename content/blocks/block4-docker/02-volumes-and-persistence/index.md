---
title: "Volumes and Persistence"
date: "2026-05-12"
weight: 30
type: docs
authors:
  - celmo
  - admin
tags:
  - Docker
  - Volumes
show_date: true
---

## Problem: Where is my result ?
As you may have noticed, a container is an isolated environment from the host machine and therefore does not share data by default.

By design, any data created inside a container is stored in its writable layer. This data persists as long as the container exists, but it is lost when the container is removed.

It can be accessed using the docker cp command, but this is not practical for regular workflows.

```bash
docker cp <container_name|container_id>:<path_on_container_where_to_copy> <path_on_host_where_to_paste>
```


This behavior can be problematic when working with data that must persist, such as:

experiment results
datasets
configuration files

## Bind mounts
Fortunately, Docker provides a mechanism to handle persistent data: **bind mounts**.

Bind mounts can be attached to a container at runtime using the -v or --mount options, allowing you to map a directory inside the container to a persistent storage location.
This creates a direct link between the host and the container.
The associated command will be something like: 
```bash
docker run -v <host_folder_path>:<container_folder_path> 
```

### Other type of volumes (for later)
Docker also provides another type of volume called named volumes:
```bash 
docker volume create my_volume
docker run -v my_volume:/data
```
These volumes are:

- managed by Docker
- not directly linked to a host folder
- commonly used by applications (e.g. databases)

We won’t use them in this course, but you will encounter them in Docker Compose and real-world applications.

## Experiments

- After mounting your volume, try to make some changes under the results folder on both side host and container.

**Note (Linux users)**: You may encounter permission issues depending on the user inside the container. This is due to UID/GID differences between host and container.

## Conclusion 

Containers are ephemeral by design.
Volumes are what make them useful in real workflows.

How can multiple containers share data?