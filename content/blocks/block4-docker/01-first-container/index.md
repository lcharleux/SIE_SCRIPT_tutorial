---
title: "Step 1: Create My First Container with Docker"
date: "2026-05-12"
weight: 20
type: docs
authors:
  - celmo
  - admin
tags:
  - Docker
  - Containers
show_date: true
---

## Official documentation

- [Docker](https://code.visualstudio.com/docs/devcontainers/containers), official documentation of Docker container.
- [Containerization](https://www.redhat.com/en/topics/cloud-native-apps/what-is-containerization), explanation about containerization from Redhat.

## How to run a Docker container ? 

You can launch a container directly from an image available online:

```bash
docker run -it python:3.11 bash
```

- **run**: creates and launches a container from an image
- **-it**: launches the container in interactive mode with an attached terminal
- **python:3.11**: Docker image containing a ready-to-use Python environment
- **bash**: program executed when the container starts, replacing the default command

When launching, Docker first looks for the image locally. If it is not present, Docker downloads it from a remote registry, DockerHub by default.

The full name of an image follows this format: [registry]/[namespace]/[repository]:[tag].
Therefore, python:3.11 is interpreted as: docker.io/library/python:3.11.

If the image comes from another registry, for example GitHub Container Registry, the full name could be:
ghcr.io/user/python:3.11

A container is an instance of an image. You can therefore launch several containers from the same image. You can use the following command to run multiple containers in detached mode. 

```bash
docker run -td python:3.11 bash
```

**Good to know**: There is a huge variety of Docker images available online on [Docker Hub](https://hub.docker.com/), for example:

- NVIDIA / CUDA / AI: `nvidia/cuda:12.2.0-runtime-ubuntu22.04`, base image with CUDA runtime, often used with frameworks like PyTorch or TensorFlow for GPU-accelerated computing.
- LaTeX `texlive/texlive:latest`, full LaTeX distribution based on TeX Live, suitable for compiling scientific documents and theses.
- ROS (Robotics), `ros:humble`, official image for ROS 2 (Robot Operating System), widely used in robotics for simulation, control, and sensor integration.


## How to run a customized Docker container ? 

At the base of a Docker container, there is a text file often called `Dockerfile`.
This text file contains all the instructions used to create a work environment isolated from your host machine.

A minimal Dockerfile example:

```Dockerfile
# Dockerfile
FROM python:3.11    # Base image
RUN pip install numpy matplotlib scipy # Instruction
CMD ["bash"]
```

Then, you have to build an image from your `Dockerfile` locate in the current directory :
```bash
docker build -t <my_image>:<my_image_tag> .
```


Now you can use `docker run` command to launch your custom container.

Let’s see how to run our [project](https://github.com/SCRIPT-SIE-2026/BLOCK4_Docker_Project.git) in a Docker container!