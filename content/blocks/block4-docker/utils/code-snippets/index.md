---
title: "Docker Code Snippets"
date: "2026-05-12"
weight: 100
type: docs
authors:
  - celmo
  - admin
tags:
  - Docker
  - Dockerfile
show_date: true
---

## Table of contents

- [Useful things to add to a dockerfile](#useful-things-to-add-to-a-dockerfile)
  - [A non-root user](#a-non-root-user)
  - [A fancy terminal](#a-fancy-terminal)
  - [A miniforge python installation from env.yml file](#a-miniforge-python-installation-from-envyml-file)

## Useful things to add to a dockerfile

### A non-root user

source: [here](https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user)
```dockerfile
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    #
    # [Optional] Add sudo support. Omit if you don't need to install software after connecting.
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# ********************************************************
# * Anything else you want to do like clean up goes here *
# ********************************************************

# [Optional] Set the default user. Omit if you want to keep the default as root.
USER $USERNAME
```

### A fancy terminal
```dockerfile
# STARSHIP INSTALL FOR NERDS
ENV RUSTUP_HOME=/opt/cargo
ENV CARGO_HOME=/opt/cargo
RUN umask 0000 && curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
RUN umask 0000 && curl -sS https://starship.rs/install.sh | sh -s -- -y
RUN echo "eval '$(starship init bash)'" >> /etc/skel/.bashrc
RUN echo "export PATH=\$PATH:/opt/cargo/bin" >> /etc/skel/.bashrc
RUN mkdir /etc/skel/.config && starship preset plain-text-symbols -o /etc/skel/.config/starship.toml
```

### A miniforge python installation from env.yml file

```dockerfile
# MINIFORGE INSTALL
RUN cd /tmp && wget "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
RUN echo $(ls /tmp/Mini*)
RUN cd /tmp && bash Miniforge3-$(uname)-$(uname -m).sh -b -p /opt/conda

COPY environment.yml /tmp/environment.yml
ENV CONDA_BIN_PATH /opt/conda/bin/conda
ENV MAMBA_BIN_PATH /opt/conda/bin/mamba
ENV CONDA_ENV_NAME container_env

RUN umask 0000 && ${MAMBA_BIN_PATH} create -y -n ${CONDA_ENV_NAME}
RUN umask 0000 && ${MAMBA_BIN_PATH} env update --file /tmp/environment.yml
RUN umask 0000 && /opt/conda/envs/${CONDA_ENV_NAME}/bin/pip  install opencv-python opencv-contrib-python
RUN echo ". /opt/conda/etc/profile.d/conda.sh" >> /etc/skel/.bashrc
RUN echo "conda activate $CONDA_ENV_NAME" >> /etc/skel/.bashrc
```




