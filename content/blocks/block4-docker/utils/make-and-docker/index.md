---
title: "Make and Docker"
date: "2026-05-12"
weight: 90
type: docs
authors:
  - celmo
  - admin
tags:
  - Docker
  - Make
show_date: true
---

## Why use `make` with Docker?

When working regularly with Docker, we often end up typing the same commands again and again:

```bash
docker build -t my-image:latest .
docker run --rm -it -p 8000:8000 my-image:latest
docker stop my-container
docker logs -f my-container
```

This works, but it quickly becomes repetitive, error-prone, and difficult to standardize across a team.

`make` allows us to turn these commands into short, readable, shared actions:

```bash
make build
make run
make stop
make logs
```

The main benefits are:

- simplifying long or hard-to-remember Docker commands;
- avoiding copy-paste mistakes or forgotten options;
- sharing the same commands across the whole project team;
- centralizing useful variables such as the image name, tag, port, or container name;
- documenting the project's common workflows in a single file: the `Makefile`.

In practice, `make` often acts as a small command-line interface on top of Docker.

## Installing `make`

### Linux (Debian-based distributions)

On Debian, Ubuntu, and other Debian-based distributions, `make` can be installed with `apt`:

```bash
sudo apt update
sudo apt install make
```

Check the installation:

```bash
make --version
```

### macOS

Two common options:

1. Install Apple's command line tools:

```bash
xcode-select --install
```

2. Or install GNU Make with Homebrew:

```bash
brew install make
```

Then verify:

```bash
make --version
```

### Windows

For Docker-based development, the simplest option is often to use **WSL**.

1. Install WSL if needed.
2. Open a Linux distribution such as Ubuntu.
3. Install `make`:

```bash
sudo apt update
sudo apt install make
```

Other possibilities:

- with Chocolatey:

```powershell
choco install make
```

- with Scoop:

```powershell
scoop install make
```

Then verify:

```bash
make --version
```

## Minimal structure

A `Makefile` is usually placed at the root of the project, at the same level as the `Dockerfile`.

Example:

```text
my-project/
├── Dockerfile
├── Makefile
└── src/
```

Each `make` target corresponds to one action.

## Example of a Docker `Makefile`

Here is a simple and reusable example for common tasks: building an image, starting a container, opening a shell, viewing logs, and cleaning up.

Important: in a `Makefile`, command lines must start with a **tab**, not spaces.

```make
IMAGE_NAME = my-app
IMAGE_TAG = latest
CONTAINER_NAME = my-app-dev

.PHONY: help build run shell stop logs clean rebuild

help:
	@echo "Available targets:"
	@echo "  make build    -> build the Docker image"
	@echo "  make run      -> start the container"
	@echo "  make shell    -> open a shell in the image"
	@echo "  make stop     -> stop the container"
	@echo "  make logs     -> show the logs"
	@echo "  make clean    -> remove the container"
	@echo "  make rebuild  -> rebuild the image without cache"

build:
	docker build -t $(IMAGE_NAME):$(IMAGE_TAG) .

run:
	docker run --rm -d \
		--name $(CONTAINER_NAME) \
		$(IMAGE_NAME):$(IMAGE_TAG)

shell:
	docker run --rm -it \
		--name $(CONTAINER_NAME)-shell \
		$(IMAGE_NAME):$(IMAGE_TAG) \
		sh

stop:
	docker stop $(CONTAINER_NAME)

logs:
	docker logs -f $(CONTAINER_NAME)

clean:
	-docker rm -f $(CONTAINER_NAME)

rebuild:
	docker build --no-cache -t $(IMAGE_NAME):$(IMAGE_TAG) .
```

## How to use it

From the project root:

```bash
make build
make run
make logs
make stop
```

If the application listens on port `8000` inside the container, it will be available at `http://localhost:8000`.

## Useful development variant

During development, it is often useful to mount the current folder inside the container so that code can be edited without rebuilding the image after every change.

Example:

```make
run-dev:
	docker run --rm -it \
		--name $(CONTAINER_NAME) \
		-p $(HOST_PORT):$(PORT) \
		-v $(PWD):/app \
		-w /app \
		$(IMAGE_NAME):$(IMAGE_TAG) \
		sh
```

This target allows you to:

- open a shell inside the container;
- access the source code mounted from the host machine;
- test commands quickly without rebuilding every time.

## Good practices

- use explicit variable names such as `IMAGE_NAME` or `CONTAINER_NAME`;
- add a `help` target to make the `Makefile` self-documented;
- declare targets with `.PHONY` to avoid conflicts with files of the same name;
- keep targets short and focused on real day-to-day actions;
- version the `Makefile` with the project so the whole team uses the same commands.

## Conclusion

`make` does not replace Docker: it makes Docker easier to use every day.

For a personal project, it saves time.
For a team project, it makes commands more reliable, more readable, and easier to share.

A good `Makefile` quickly becomes a very practical entry point for:

- building an image;
- starting a container;
- opening a shell;
- viewing logs;
- cleaning the local environment.
