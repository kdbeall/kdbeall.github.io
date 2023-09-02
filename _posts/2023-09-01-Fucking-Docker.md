---
layout: post
title: Docker Notes
---

## Installation and Configuration

### **Supported Platforms**
* Docker Desktop is available for Windows and macOS. It provides an integrated GUI and CLI environment.
* Docker Server can be installed on many Linux distributions, including Ubuntu, CentOS, Debian, Fedora, and others. It can also be installed on cloud platforms like AWS and Azure.

### **Installation**
Follow whatever instructions for your platform.

### **Post-Installation Steps**

- **Start Docker**:
  - Desktop platforms: Start Docker Desktop application.
  - Linux: Ensure Docker service is running.

- **Verify Installation**:
  - Check version: `docker --version`
  - Test run: `docker run hello-world`

- **User Permissions**:
  - Default: Docker needs root privileges.
  - Linux: Add user to `docker` group to avoid using `sudo` (caution advised).

### **Configuration**

- **Docker Daemon**:
  - Configuration file: `/etc/docker/daemon.json`
  - Allows configuration of the Docker daemon behavior.

- **Docker CLI**:
  - Configured using environment variables like `DOCKER_HOST`.

- **Remote Access**:
  - Default: Docker listens on a Unix socket.
  - Caution needed if configuring Docker to listen on a TCP socket for remote access.

- **Storage**:
  - Uses storage drivers (e.g., overlay2, aufs, btrfs).
  - Choose based on performance or compatibility.

- **Networking**:
  - Default bridge network for containers.
  - Configuration options include setting default subnet, gateway, and DNS.

## Image Creation, Management, and Registry

### **Dockerfiles**
- Docker images are often created using a `Dockerfile`.
- Contains instructions for building the image.
- Common instructions: `FROM`, `RUN`, `COPY`, `CMD`.

### **Building Images**
- Use the `docker build` command.
  ```bash
  docker build -t my_image_name:my_tag .
  ```
### **Listing Images**
- List available images with `docker images` or `docker image ls`.

### **Removing Images**
- Remove an image with `docker rmi my_image_name:my_tag`

### **Tagging an Image**
- Tag an image with `docker tag source_image:tag new_image:new_tag`

### **Inspect an Image**
- Inspect an image with `docker inspect my_image_name:my_tag`

## Orchestration
Todo

## Networking
Todo

## Storage and Volumes
Todo

## Security
Todo
