---
title: "Docker Compose Commands Cheatsheet"
date: "2026-05-12"
weight: 70
type: docs
authors:
  - celmo
  - admin
tags:
  - Docker Compose
  - Cheatsheet
show_date: true
---

This sheet gathers the most useful Docker Compose commands for Phase 3.

Docker Compose commands must be run from the directory containing the `compose.yml` file.
For the course project, this means:

```bash
cd SCRIPT_SIE_2026_05_12_Project
```

Notation used:

- `<service>`: name of a service defined in `compose.yml`, for example `compute` or `report`.
- `<container>`: identifier or name of a container.

## Start Services

Start all services defined in `compose.yml`:

```bash
docker compose up
```

Start all services and rebuild images before running them:

```bash
docker compose up --build
```

Start all services in the background:

```bash
docker compose up -d
```

For the course pipeline, this runs the computation service and then the report service:

```bash
docker compose up --build
```

## Stop and Remove Services

Stop running services without removing their containers:

```bash
docker compose stop
```

Stop and remove the containers created by Docker Compose:

```bash
docker compose down
```

`docker compose down` removes the containers, but it does not remove bind-mounted project files such as the `results/` directory.

## List Services and Containers

List the services and containers managed by Docker Compose:

```bash
docker compose ps
```

List all containers, including stopped Compose containers:

```bash
docker ps -a
```

## Logs

Show logs for all services:

```bash
docker compose logs
```

Follow logs in real time:

```bash
docker compose logs -f
```

Show logs for one service:

```bash
docker compose logs compute
```

Show logs for the LaTeX report service:

```bash
docker compose logs report
```

## Run One Service

Run only one service and remove the container when it stops:

```bash
docker compose run --rm <service>
```

Example:

```bash
docker compose run --rm compute
```

Run an interactive shell in a service image:

```bash
docker compose run --rm <service> bash
```

Example:

```bash
docker compose run --rm compute bash
```

## Execute a Command in a Running Service

Run a command inside a running service container:

```bash
docker compose exec <service> <command>
```

Example:

```bash
docker compose exec compute bash
```

This requires the service container to already be running.

## Build Images

Build or rebuild images defined with a `build:` section:

```bash
docker compose build
```

Build one service:

```bash
docker compose build compute
```

## Inspect the Configuration

Check and display the final Compose configuration:

```bash
docker compose config
```

This is useful for detecting YAML syntax errors or checking how Docker Compose interprets your file.

## Cleanup

Remove stopped Compose containers:

```bash
docker compose down
```

Remove stopped Compose containers and anonymous volumes created by Compose:

```bash
docker compose down --volumes
```

Use `--volumes` with caution: volumes may contain data that you want to keep.
