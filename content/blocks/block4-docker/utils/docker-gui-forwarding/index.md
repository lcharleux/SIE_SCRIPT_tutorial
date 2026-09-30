---
title: "Docker GUI Forwarding Guide"
date: "2026-05-12"
weight: 110
type: docs
authors:
  - celmo
  - admin
tags:
  - Docker
  - GUI
show_date: true
---

## Table of Contents

- [Linux](#linux)
- [Windows + WSL2](#windows--wsl2)
  - [Windows 11 (WSLg)](#windows-11-wslg)
  - [Windows 10 + VcXsrv](#windows-10--vcxsrv)
- [macOS](#macos)
  - [Intel and Apple Silicon](#intel-and-apple-silicon)
- [Useful Test Applications](#useful-test-applications)
- [Common Errors](#common-errors)

---

# Linux

## X11 Forwarding

Allow Docker to access the local X server:

```bash
xhost +local:docker
```

Run the container:

```bash
docker run --rm -it \
  -e DISPLAY=$DISPLAY \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  debian:12 bash
```

Inside the container:

```bash
apt update
apt install -y x11-apps
xeyes
```

Revoke access:

```bash
xhost -local:docker
```

---

## More Secure Variant (XAUTHORITY)

```bash
docker run --rm -it \
  -e DISPLAY=$DISPLAY \
  -e XAUTHORITY=/tmp/.Xauthority \
  -v $HOME/.Xauthority:/tmp/.Xauthority:ro \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  debian:12
```

---

## Wayland

Check your session type:

```bash
echo $XDG_SESSION_TYPE
```

Most GUI Docker setups on Wayland still rely on XWayland.

---

# Windows + WSL2

# Windows 11 (WSLg)

WSLg already provides GUI forwarding.

Run:

```bash
docker run --rm -it \
  -e DISPLAY=$DISPLAY \
  -e WAYLAND_DISPLAY=$WAYLAND_DISPLAY \
  -e XDG_RUNTIME_DIR=$XDG_RUNTIME_DIR \
  debian:12 bash
```

Inside the container:

```bash
apt update
apt install -y x11-apps
xeyes
```

No `/tmp/.X11-unix` bind mount is usually required.

---

# Windows 10 + VcXsrv

## Install VcXsrv

Install:

- https://sourceforge.net/projects/vcxsrv/

Launch:

```text
XLaunch
```

Recommended options:

- Multiple windows
- Start no client
- Disable access control

---

## Configure DISPLAY

Inside WSL2:

```bash
export DISPLAY=$(grep nameserver /etc/resolv.conf | awk '{print $2}'):0
```

Optional for some OpenGL apps:

```bash
export LIBGL_ALWAYS_INDIRECT=1
```

---

## Run Container

```bash
docker run --rm -it \
  -e DISPLAY=$DISPLAY \
  -e LIBGL_ALWAYS_INDIRECT=1 \
  debian:12 bash
```

Inside the container:

```bash
apt update
apt install -y x11-apps
xclock
```

---

# macOS

# Intel and Apple Silicon

## Install XQuartz

Install:

- https://www.xquartz.org/

Launch XQuartz.

Enable:

```text
XQuartz → Settings → Security → Allow connections from network clients
```

Restart XQuartz.

---

## Allow Connections

```bash
xhost +localhost
```

---

## Run Container

```bash
docker run --rm -it \
  -e DISPLAY=host.docker.internal:0 \
  debian:12 bash
```

Inside the container:

```bash
apt update
apt install -y x11-apps
xeyes
```

No `/tmp/.X11-unix` bind mount is required on macOS.

---

## Apple Silicon Notes

Most official images support ARM64 natively.

Only force emulation if needed:

```bash
docker run --platform linux/amd64 ...
```

---

# Useful Test Applications

Install:

```bash
apt install -y x11-apps
```

Examples:

| Command | Description |
|---|---|
| xeyes | Eyes following cursor |
| xclock | Analog clock |
| xcalc | Calculator |
| xlogo | X11 logo |

---

# Common Errors

## Cannot Open Display

Example:

```text
Error: Can't open display
```

Possible causes:

- DISPLAY not configured
- X server not running
- Missing authorization
- Missing X11 socket bind mount on Linux

---

## No Protocol Specified

Usually an authorization issue.

Linux:

```bash
xhost +local:docker
```

macOS:

```bash
xhost +localhost
```

---

## Wayland Issues

Force X11 backend:

```bash
export GDK_BACKEND=x11
```

---

# Summary

| Platform | GUI Forwarding Method |
|---|---|
| Linux | X11 Unix socket |
| Windows 11 | WSLg |
| Windows 10 | VcXsrv over TCP |
| macOS Intel | XQuartz over TCP |
| macOS Apple Silicon | XQuartz over TCP + ARM64 |
