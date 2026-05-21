---
title: "Docker Compose"
date: "2026-05-12"
weight: 40
type: docs
authors:
  - celmo
  - admin
tags:
  - Docker
  - Docker Compose
show_date: true
---

## Why Docker Compose?

So far, we have been able to launch a Python computation container.
This container produced results that we were able to retrieve and persist using volumes.

It would now be useful to add another container to the workflow: for example, a LaTeX container that takes these results and integrates them into a scientific document.

We now want to go one step further.
Our workflow is no longer a single container:
- one container generates results (Python),
- another one could use these results (for example, to produce a report).

So the questions are:
- **How do we manage multiple containers working together?**

- **How do we avoid writing complex `docker run` commands for each step?**


`Docker Compose` is one possible answer to this problem and is designed for this kind of situation.
It allows us to define and run a multi-container application using a single configuration file.

Instead of writing long `docker run` commands by hand, we describe the services, images, volumes, environment variables, and execution order in a `compose.yml` file.

## From `docker run` to Docker Compose

Docker Compose is configured using a YAML file called `compose.yml`.
You may also encounter the older name `docker-compose.yml`.

Before discussing orchestration between multiple containers, Docker Compose already makes it easier to start a single container, especially when it has many launch arguments.

For example, the following command:

```bash 
docker run --rm -it \
  --name <container_name> \
  -v <host_folder>:<container_folder> \
  <image_name>:<image_tag> \
  <command>
```

can be written as the following `compose.yml` file:

```yaml
services:
  compute: # service name mandatory
    image: <image_name>:<image_tag>
    container_name: <container_name> # optional
    volumes:
      - <host_folder>:<container_folder>
    command: <command>
```

You can also pass directly your `Dockerfile` to launch a container with Docker compose, avoiding you to build and named your image with `docker build` process:

```yaml
services:
  compute:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: <container_name> # optional
    volumes:
      - <host_folder>:<container_folder>
    command: <command>
```

Now you can use `docker compose` commands such as `docker compose up`, `docker compose stop` or `docker compose down` to control your container, see [Docker compose commands cheatsheet](../cheatsheets/docker-compose-commands/) for more details. 

**Note**: `docker compose stop` only stops containers.
`docker compose down` removes the containers, but it does not remove your project files or bind-mounted results.


### Exercise

Try to run the computation container from the project repository using `docker compose` tool.

## Running Several Containers

Let us now describe a small pipeline made of two services:

- `compute`: runs the Python script and generates `results/figure.png`;
- `report`: compiles the LaTeX document using the generated figure.

Both services mount the same project directory at `/app`.
This is how the LaTeX container can access the figure produced by the Python container.

Create the following `compose.yml` file at the root of the project repository:

```yaml
services:
  compute:
    build:
      context: .
      dockerfile: Dockerfile
    working_dir: /app
    volumes:
      - .:/app
    command: sh -c "mkdir -p results && python src/compute.py"

  report:
    image: texlive/texlive:latest
    depends_on:
      compute:
        condition: service_completed_successfully
    working_dir: /app
    volumes:
      - .:/app
    command: sh -c "cd report && pdflatex -output-directory=../results main.tex"
```

Then run:

```bash
docker compose up --build
```

The expected output is:

```text
results/
|-- figure.png
`-- main.pdf
```

The `depends_on` section controls the order:

```yaml
depends_on:
  compute:
    condition: service_completed_successfully
```

This means that the `report` service starts only if the `compute` service finishes successfully.
If the Python computation fails, the LaTeX compilation should not start.

## Useful Docker Compose Commands
A list of useful Docker Compose commands is available [here](../cheatsheets/docker-compose-commands/).


## Exercise

1. Create a `compose.yml` file in the project repository.
2. Add the `compute` service.
3. Run the service and check that `results/figure.png` is created.
4. Add the `report` service.
5. Run the full pipeline with `docker compose up --build`.
6. Check that the PDF report is created in the `results/` directory.
7. Try to multiple figures and to enhance your latex report.

## Conclusion

Docker Compose is useful when a project is made of several containers that must work together.
In our case, one container runs the computation and another one compiles the report.

The important point is that each container keeps its own environment, while volumes allow them to share files when needed.
