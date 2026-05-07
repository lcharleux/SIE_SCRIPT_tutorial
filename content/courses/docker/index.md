---
title: "Block 4: Docker for Reproducible Research Environments"
date: "2026-05-12"
publishDate: "2026-01-01"
links:
  - type: site
    url: https://adum.fr/script/catalogue.pl?mod=3739713&site=USMB
    name: "Registration for training on Adum"
tags:
  - Docker
  - Python
  - GIT
authors:
  - celmo
  - admin
show_date: true
---

Containerization enables portable, isolated computational environments that improve the reproducibility, transparency, and longevity of research. This module introduces Docker for constructing, executing, and sharing environments that consistently reproduce analyses across machines and over time.

## Learning outcomes

By the end of the session, participants will be able to:

- Explain core concepts (images, containers, registries) and distinguish containers from virtual machines.
- Author reproducible images with `Dockerfile`, including pinning versions and managing build context and caching.
- Run containers with appropriate configuration (volumes, environment variables, ports, resource limits).
- Package notebooks, command‑line tools, and dependencies for consistent execution and sharing.
- Use Docker Compose for simple multi‑service setups where appropriate.
- Publish and retrieve images from container registries (e.g., Docker Hub, GHCR) with tagged versions.
- Apply containerization to research workflows for archiving, review, and publication.

## Topics

- Reproducible environments: motivation and principles
- Images and layers; `Dockerfile` patterns (base images, multi‑stage builds, minimal images)
- Data and state: bind mounts vs. volumes; handling large data
- Interactive workflows: Jupyter in containers; connecting to GPUs/accelerators when available
- Sharing and provenance: tags, digests, and registries
- Good practices for research projects: directory structure, `.dockerignore`, licensing and metadata

## Prerequisites

- Basic command‑line familiarity; Git recommended for version control.
- Administrative install permissions on your computer (Windows, macOS, or Linux).
- Ability to install Docker Desktop or Docker Engine and run: `docker --version` and `docker run hello-world`.

## Installation Instructions

A. Hardware requirements:
- 64-bit processor
- 8 GB system RAM recommended
- At least 20 GB of free disk space
- Enable hardware virtualization in BIOS/UEFI. For more information, see [Virtualization](https://docs.docker.com/desktop/troubleshoot-and-support/troubleshoot/topics/#docker-desktop-fails-due-to-virtualization-not-working).

B. Software requirements:
- Git, [see the Git installation instructions](https://lcharleux.github.io/SIE_SCRIPT_tutorial/courses/git/#installation-instructions).
- VS Code. Windows users should choose the System Installer version from the [VS Code download page](https://code.visualstudio.com/download).

Make sure your computer meets these requirements before the session.

C. Docker Desktop

For this training session, we will install Docker through Docker Desktop. It provides both the Docker command-line tools and a graphical interface, which can be useful when learning.


{{< spoiler text="Windows" >}}

  1. **We strongly recommend enabling the WSL 2 backend first.** You can follow the official Microsoft guide [here](https://learn.microsoft.com/fr-fr/windows/wsl/install).

  Open PowerShell with administrator rights: right-click PowerShell and select "Run as administrator".

  - Set WSL 2 as default: 
    ```powershell
    wsl.exe --set-default-version 2
    ```

  - Install a version of Ubuntu (by default)
    ```powershell
    wsl.exe --install
    ```
    During installation, you will be asked to provide a username and password for this virtual machine.
    Once installation is complete, you should be logged in to your Ubuntu virtual machine.

  2. Download and install Docker Desktop for Windows from the [official Docker documentation](https://docs.docker.com/desktop/setup/install/windows-install/).
  During the installation, make sure "Use WSL 2 instead of Hyper-V" is selected.
  At the end of the installation, you may need to restart your computer or sign out and sign back in.
  You do not need a Docker Hub account for this session, so you can skip the sign-in step.
  
{{< /spoiler >}}

{{< spoiler text="macOS" >}}
  Follow the official Docker Desktop for macOS installation instructions [here](https://docs.docker.com/desktop/setup/install/mac-install/).

{{< /spoiler >}}

{{< spoiler text="Linux (Ubuntu/Debian-based)" >}}
  
  - On Ubuntu, you can install Docker Desktop by following the official instructions [here](https://docs.docker.com/desktop/setup/install/linux/ubuntu/).
  - If you install Docker Engine instead of Docker Desktop, follow the Linux post-installation steps [here](https://docs.docker.com/engine/install/linux-postinstall/) so that you can run `docker` commands without `sudo`.

{{< /spoiler >}}

Whatever your operating system, you can check that Docker is installed by typing the following command into your terminal (PowerShell for Windows users): 

```shell
docker run hello-world
```

Normally, you should see the following output:
```output
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
58dee6a49ef1: Pull complete 
c3bdf82c34d1: Download complete 
Digest: sha256:f9078146db2e05e794366b1bfe584a14ea6317f44027d10ef7dad65279026885
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.
```

## Format

The session combines a concise conceptual overview with guided, hands‑on exercises using research‑relevant examples. Templates are provided to facilitate adaptation to participants’ projects.

<!--more-->
