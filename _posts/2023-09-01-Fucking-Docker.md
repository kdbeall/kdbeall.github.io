---
layout: post
title: Docker Notes
---

This is a quick overview of Docker and I'm aiming to largely encapsulate the material held in the Docker Certified Associate exam.
I might eventually follow-up with a Docker Notes Part II. 

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

### Docker Swarm
Eventually I'll consider adding this in.

___

## Networking

### Types of Networks
There are a varity of networking options in Docker.

####  **Bridge Network**
- Default network driver.
- When you run a container without specifying any network options, it attaches to this bridge network.
- Containers can access each other and the host machine over the bridge network, but need port mapping for external access.

#### **User-defined Bridge Network**
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

One of the key principles of Docker containers is their ephemerality. Containers can be stopped, destroyed, and recreated with the assurance that they'll run the same way every time, provided the image remains consistent. Volumes and bind mounts facilitate this by allowing data to be persisted and shared across containers, without baking the data directly into the container image.

### **Storage Drivers**
* Docker has the capability to use different storage drivers based on the host system. These drivers handle the details of allocating storage and managing the file system. Some popular storage drivers include overlay2, aufs, devicemapper, btrfs, and zfs.
* The choice of storage driver can influence the performance and the way storage is handled for containers. overlay2 is often recommended for many setups due to its performance characteristics and compatibility.

### **Volumes**
Volumes are the preferred mechanism for persisting data generated by and used by Docker containers. 
Volumes have several advantages:

- Life Cycle Independence: Volumes are designed to exist independently of the container's life cycle. This means even if you delete a container, the volume associated with it can still persist.
- Performance: They offer better performance than other storage options such as bind mounts.
- Backup, Restore, or Migrate Data: Volumes can be easily backed up, restored, or migrated to different Docker hosts.

### **Volume Commands**
- Create a Volume: `docker volume create my_volume`
- Mount a Volume to a container: `docker run -d -v my_volume:/path/in/container my_image`

### **Bind Mounts**
* Are a mapping of a host file or directory to a container file or a directory.
- Create a Bind Mount: `docker run -d -v /path/on/host:/path/in/container my_image`

### **tmpfs Mounts**
* A tmpfs Mount allow creating a temporary file system into the container's memory, which can be useful for sensitive information or cache storage. The data doesn't persist beyond the container's lifecycle.
- Create a tmpfs Mount: `docker run -d --tmpfs /tmp my_image`

### **Storage Commands and Inspection**
- List Volumes: `docker volume ls`
- Inspect a Volume: `docker volume inspect my_volume`
- Remove a Volume: `docker volume rm my_volume`

___

## Security


### **Namespaces**
* Containers use namespaces to provide isolation. 
* Namespaces ensure that containers have their view of the system, without interfering with other containers.
* Types: PID (process), NET (network), IPC (Interprocess Communication), MNT (mount), UTS (hostname), and USER (UIDs).

### **Control Groups (cgroups)**
* Limit and monitor resource usage (CPU, memory, I/O, etc.) for containers.
* Ensure that no single container can monopolize system resources.

### **Capabilities**
* Linux capabilities allow you to grant certain privileges to processes without giving them full root access.
* Docker drops many capabilities by default and allows users to add only specific ones, reducing the risk.

### **Secure Computing Mode (seccomp)**
* Filters system calls a process (or container) is allowed to make, enhancing the confinement of the container.

### **Image Security**
* Trusted Content: Use trusted base images, preferably from official sources on Docker Hub or other trusted registries.
* Image Signing: Docker Content Trust (DCT) allows you to sign and verify the integrity of images.
* Vulnerability Scanning: Tools like Clair can scan Docker images for known vulnerabilities.

#### *Runtime Security*
* Run containers with read-only file systems when possible to prevent unwanted changes.
* Limit the capabilities given to containers to only those they strictly need.
* Use cgroups to limit memory, CPU, and I/O usage for containers.

#### *Networking Security*
* Enable TLS for the Docker daemon to ensure encrypted and authenticated communication.
* The Docker daemon socket (/var/run/docker.sock) should be protected and accessible only by trusted users. Exposure can grant full control over Docker.
* Limit Docker API access, enable user namespaces, and set the default seccomp profile.

### **Orchestration & Cluster Security**
* In swarm mode or Kubernetes, use RBAC to limit access and actions that users and services can perform.
* Use Docker secrets or other tools to manage and securely distribute sensitive data.
* In swarm mode, ensure encrypted communication between nodes using the --opt encrypted flag.

### **Logging & Monitoring**
* Use centralized logging solutions to monitor container activities.
* Implement audit logging to keep track of actions performed on the Docker daemon or within the cluster.

### **Updates & Patch Management**
* Regularly update the Docker engine, services, and containers to benefit from security patches.
* Keep the host OS patched and minimize its footprint.
* Use a minimal and security-hardened host OS, like Alpine Linux, CoreOS, or RancherOS.
