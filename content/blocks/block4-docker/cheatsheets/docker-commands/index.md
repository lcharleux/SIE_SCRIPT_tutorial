---
title: "Docker Commands Cheatsheet"
date: "2026-05-12"
weight: 60
type: docs
authors:
  - celmo
  - admin
tags:
  - Docker
  - Cheatsheet
show_date: true
---

This sheet gathers the most useful Docker commands for the course.

For Docker Compose commands used in Phase 3, see [Docker Compose commands cheatsheet](../docker-compose-commands/).

Notation used:

- `<image>`: name of a Docker image, for example `python:3.11`.
- `<container>`: identifier or name of a container.
- `<volume>`: name of a Docker volume.
- `<network>`: name of a Docker network.
- `<host_path>`: path on your machine.
- `<container_path>`: path inside the container.

## Table of Contents

- [Docker Images](#docker-images)
- [Build an Image from a Dockerfile](#build-an-image-from-a-dockerfile)
- [Launch a Container](#launch-a-container)
- [Stop a container](#stop-a-container)
- [List Containers](#list-containers)
- [Interact with a Container](#interact-with-a-container)
- [View Logs and Detailed Information](#view-logs-and-detailed-information)
- [Manage a Container's State](#manage-a-containers-state)
- [Remove Containers](#remove-containers)
- [Volumes](#volumes)
- [Copy Files](#copy-files)
- [Networks](#networks)
- [Cleanup and Disk Space](#cleanup-and-disk-space)

## Docker Images

Download an image from a registry, for example Docker Hub:

```bash
docker pull python:3.11
```

List the images available locally:

```bash
docker images
```

Equivalent command, more consistent with Docker's modern subcommands:

```bash
docker image ls
```

Remove a local image:

```bash
docker image rm <image>
```

Equivalent short form:

```bash
docker rmi <image>
```

Example:

```bash
docker rmi python:3.11
```

An image cannot be removed if it is still used by an existing container.

## Build an Image from a Dockerfile

Build an image from the `Dockerfile` located in the current directory:

```bash
docker build -t <image_name>:<tag> .
```

Example for the course project:

```bash
cd SCRIPT_SIE_2026_05_12_Project
docker build -t sci-project:latest .
```

The `.` tells Docker to use the current directory as the build context.
It means that Docker can access the files in the current directory when building the image.

## Launch a Container

Launch a container in interactive mode with an attached terminal:

```bash
docker run -it <image> <command>
```

Example:

```bash
docker run -it python:3.11 bash
```

Launch a container in the background:

```bash
docker run -d <image>
```

Launch a container in the background with an allocated terminal:

```bash
docker run -td <image> <command>
```

Example:

```bash
docker run -td python:3.11 bash
```

Give the container a name:

```bash
docker run --name <container_name> -it <image> <command>
```

Example:

```bash
docker run --name python-test -it python:3.11 bash
```

Automatically remove the container when it stops:

```bash
docker run --rm -it python:3.11 bash
```

Launch the image built in the course project:

```bash
docker run --rm sci-project:latest
```

Mount the current directory inside the container:

```bash
docker run --rm -it -v "$PWD:/app" -w /app python:3.11 bash
```

Run the course project while mounting the current directory:

```bash
docker run --rm -it \
  --name sci-project \
  -v "$PWD:/app" \
  -w /app \
  sci-project:latest \
  sh -c "mkdir -p results && python src/compute.py"
```

Important options:

- `-i`: keeps standard input open.
- `-t`: allocates a terminal.
- `-d`: runs the container in the background.
- `--name`: gives the container a readable name.
- `--rm`: removes the container when it stops.
- `-v`: mounts a volume or local directory.
- `-w`: sets the working directory inside the container.
- `-e`: defines an environment variable.

## Stop a container

Stop a container: 

```bash
docker stop <container_name or container_ID>
```

Remove a container (container need to be stopped first): 

```bash
docker rm <container_name or container_ID>
```

Stop all alive containers:

```bash
docker stop $(docker ps -q)
```

Remove all stoped containers:
```bash
docker stop $(docker ps -aq)
```

## List Containers

List running containers:

```bash
docker ps
```

List all containers, including stopped ones:

```bash
docker ps -a
```

Equivalent command:

```bash
docker container ls
```

List all containers with the `container` syntax:

```bash
docker container ls -a
```

## Interact with a Container

Run a command in an already running container:

```bash
docker exec <container> <command>
```

Open a shell in an already running container:

```bash
docker exec -it <container> bash
```

Example:

```bash
docker exec -it python-test bash
```

Attach to the main process of a container:

```bash
docker attach <container>
```

Warning: with `attach`, exiting with `Ctrl+C` may stop the container's main process. To open a shell in a running container, `docker exec -it` is often more appropriate.

## View Logs and Detailed Information

Display a container's logs:

```bash
docker logs <container>
```

Follow logs in real time:

```bash
docker logs -f <container>
```

Display detailed information about a container, image, volume, or network:

```bash
docker inspect <object>
```

Examples:

```bash
docker inspect python-test
docker inspect python:3.11
```

## Manage a Container's State

Stop a container cleanly:

```bash
docker stop <container>
```

Start a stopped container:

```bash
docker start <container>
```

Restart a container:

```bash
docker restart <container>
```

Force a container to stop immediately:

```bash
docker kill <container>
```

In practice, prefer `docker stop`. Use `docker kill` only if the container no longer responds.

## Remove Containers

Remove a stopped container:

```bash
docker rm <container>
```

Equivalent command:

```bash
docker container rm <container>
```

Remove all stopped containers with Docker's cleanup command:

```bash
docker container prune
```

Docker asks for confirmation before removing containers.

If a container is still running, stop it before removing it:

```bash
docker stop <container>
docker rm <container>
```

## Volumes

Volumes preserve data independently of a container's lifecycle.
In this course, we mainly use bind mounts to share files between the host machine and a container.

Mount a host directory inside a container:

```bash
docker run --rm -it -v <host_path>:<container_path> <image> <command>
```

Example with the current directory:

```bash
docker run --rm -it -v "$PWD:/app" -w /app python:3.11 bash
```

Mount a host directory as read-only:

```bash
docker run --rm -it -v "$PWD/data:/app/data:ro" python:3.11 bash
```

The `:ro` suffix means that the container can read the directory but cannot write to it.

Docker also supports named volumes.
They are managed by Docker and are not directly linked to a specific host folder.

List Docker volumes:

```bash
docker volume ls
```

Create a volume:

```bash
docker volume create <volume>
```

Display detailed information about a volume:

```bash
docker volume inspect <volume>
```

Use a volume in a container:

```bash
docker run --rm -it -v <volume>:/data python:3.11 bash
```

Remove a volume:

```bash
docker volume rm <volume>
```

A volume cannot be removed if it is still used by a container.

## Copy Files

Copy a file or directory from a container to the host machine:

```bash
docker cp <container>:<container_path> <host_path>
```

Example:

```bash
docker cp sci-project:/app/results ./results
```

Copy a file or directory from the host machine to a container:

```bash
docker cp <host_path> <container>:<container_path>
```

This is useful for inspection or debugging, but regular workflows should prefer bind mounts or Docker Compose.

## Networks

Docker creates networks to allow containers to communicate with each other.

List Docker networks:

```bash
docker network ls
```

Display detailed information about a network:

```bash
docker network inspect <network>
```

Example:

```bash
docker network inspect bridge
```

In this course, it is mainly useful to know how to inspect networks created automatically by Docker or Docker Compose.

## Cleanup and Disk Space

Display the disk space used by Docker:

```bash
docker system df
```

Remove unused Docker objects:

```bash
docker system prune
```

This command removes stopped containers, unused networks, and unused images in particular. Docker asks for confirmation before removing them.

Also remove unused volumes:

```bash
docker system prune --volumes
```

Use with caution: volumes may contain results or data that you want to keep.
