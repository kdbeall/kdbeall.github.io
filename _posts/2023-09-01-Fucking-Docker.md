---
layout: post
title: Docker Notes
---

## Installation and Configuration

### **Supported Platforms**
* Docker Desktop is available for Windows and macOS. It provides an integrated GUI and CLI environment.
* Docker Server can be installed on many Linux distributions, including Ubuntu, CentOS, Debian, Fedora, and others. It can also be installed on cloud platforms like AWS and Azure.

### **Installation**
* Follow whatever instructions for your platform.

___

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

___

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

___

## Image Creation, Management, and Registry

### **Dockerfiles**
- Docker images are often created using a `Dockerfile`.
- Contains instructions for building the image.
- Common instructions: `FROM`, `RUN`, `COPY`, `CMD`.

### **Building Images**
- Use the `docker build` command e.g. `docker build -t my_image_name:my_tag .`

### **Listing Images**
- List available images with `docker images` or `docker image ls`.

### **Removing Images**
- Remove an image with `docker rmi my_image_name:my_tag`

### **Tagging an Image**
- Tag an image with `docker tag source_image:tag new_image:new_tag`

### **Inspect an Image**
- Inspect an image with `docker inspect my_image_name:my_tag`

___

## Orchestration
Not much to say here yet. Kubernetes seems to be the standard.

### Docker Swarm (for exam purposes)
Todo

___

## Networking
This section will be a whopper. I can almost 

####  **Bridge Network**
- Default network driver.
- When you run a container without specifying any network options, it attaches to this bridge network.
- Containers can access each other and the host machine over the bridge network, but need port mapping for external access.

### **User-defined Bridge Network**
- Allows containers to communicate with each other.
- Useful because containers can communicate with each other using container names (DNS-based service discovery).

#### **Host Network**
- Removes network isolation between the container and the Docker host.
- The container uses the host machine’s network stack directly.

#### **Overlap Network**
- Used in Docker Swarm to enable swarm services to communicate with each other.
- Allows containers on different nodes to communicate as if they are on the same host.

#### **None Network**
- Completely disables the container's networking stack. Useful for containers which should be isolated.

#### **Macvlan Network**
- Assigns a MAC address to a container, making it appear as a physical device on the network.
- Useful for applications that need to be directly integrated into the host's physical network.

### **Networking Commands**
- List Networks: `docker network ls`
- Inspect Network: `docker network inspect [network_name]`
- Create Network: `docker network create --driver [network_driver] [network_name]`
- Remove Network: `docker network rm [network_name]`
- Connect Container: `docker network connect [network_name] [container_name/id]`
- Disconnect Container: `docker network disconnect [network_name] [container_name/id]`

___

## Storage and Volumes
Todo

___

## Security
Todo
