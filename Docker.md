# Docker Notes
## What is Docker?
Docker is an operating system for containers. Similar to how a virtual machine virtualizes (removes the need to directly manage) server hardware, containers virtualize the operating system of a server. Docker is installed on each server and provides simple commands you can use to build, start, or stop containers.

## What is image?
A Docker image is a read-only template that contains a complete, self-contained snapshot of an application and its entire environment, including the operating system, libraries, dependencies, and application code. It serves as a blueprint for creating Docker containers.

## What is container?
A Docker container is a runnable instance of a Docker image. It is a lightweight, standalone, and executable software package that encapsulates an application and all its necessary components, including code, dependencies, libraries, and configuration files

## Why We Use Docker?

When multiple users work on a project, dependency conflicts can occur. For example:

```
User 1 (dependency v1)
   │
   ├─> push ──> GitHub
                 │
                 └─> pull ──> User 2 (dependency v2)
                                   │
                                   ├─> push ──> GitHub
                                                 │
                                                 └─> AWS (deployment)
```

- **Problem:** User 1 and User 2 may use different versions of dependencies. When deploying to AWS, this can cause conflicts and failures.

**Docker Solution:**

Docker packages the application and all its dependencies into a container. This ensures everyone uses the same environment, eliminating "it works on my machine" issues.

```
User 1 ──┐
         │
User 2 ──┼─> Build Docker Image (with all dependencies)
         │
CI/CD ───┘
         │
         └─> Push Docker Image ──> AWS (runs the same everywhere)
```

### Benefits of Docker

- **Consistency:** Same environment for all users and deployments.
- **Isolation:** No conflicts between dependencies.
- **Portability:** Runs on any system with Docker.
- **Efficiency:** Lightweight compared to VMs.
- **Simplified Deployment:** Easy to distribute and



## Difference Between Docker and Virtual Machine

| Feature        | Docker (Containers)          | Virtual Machine (VM)       |
| -------------- | ---------------------------- | -------------------------- |
| OS Level       | Shares host OS kernel        | Runs full guest OS         |
| Resource Usage | Lightweight, less overhead   | Heavy, more resource usage |
| Startup Time   | Seconds                      | Minutes                    |
| Isolation      | Process-level                | Hardware-level             |
| Portability    | Highly portable              | Less portable              |
| Use Case       | Microservices, CI/CD, DevOps | Legacy apps, full OS needs |

### Structural Difference: Docker vs Virtual Machine

#### Virtual Machine Architecture

```
+---------------------+
|   App 1   |  App 2  |
+---------------------+
| Guest OS  | Guest OS|
+---------------------+
|   Hypervisor        |
+---------------------+
|   Host OS           |
+---------------------+
|   Hardware          |
+---------------------+
```
- Each VM runs its own full OS (Guest OS) on top of the hypervisor, which sits on the host OS and hardware.

#### Docker (Container) Architecture

```
+-----------------------------+
| App 1 | App 2 | App 3       |
+-----------------------------+
|      Docker Engine          |
+-----------------------------+
|         Host OS             |
+-----------------------------+
|         Hardware            |
+-----------------------------+
```
- All containers share the same OS kernel via Docker Engine, making them lightweight and fast.

**Summary:**  
- **VMs:** Each app runs in its own OS, more resource usage.
- **Docker:** Apps share the host OS, less overhead, faster

**DOCKER**
Docker is Linux-based, but we can run containers on Windows and Mac using the Docker Engine. 

**Docker Engine** is the core software that creates and manages containers. On Windows and Mac, Docker Engine runs inside a lightweight virtual machine that provides a Linux environment. This allows Docker containers to run seamlessly, regardless of the host operating system. 

- On Windows/Mac, Docker Desktop manages this VM automatically.
- Users interact with Docker the same way as on Linux.

This makes Docker containers portable and consistent across all platforms.

## Installing Docker from Docker Hub

1. Go to [https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)
2. Download Docker Desktop for your OS (Windows/Mac).
3. Run the installer and follow the setup instructions.
4. After installation, verify with:
   ```
   docker --version
   ```

---

## Difference Between Docker Image and Docker Container

| Docker Image                          | Docker Container                      |
|----------------------------------------|---------------------------------------|
| Blueprint or template for containers   | Running instance of an image          |
| Read-only                              | Read-write (can change state)         |
| Stored on disk                         | Runs in memory                        |
| Can create many containers from image  | Created from an image                 |

---

## Basic Docker Commands

### Pull an Image from Docker Hub

```
docker pull <image_name>
```
Example:
```
docker pull nginx
```

### Create and Run a Container

```
docker run <image_name>
```
Example:
```
docker run nginx
```

- To run in detached mode (background):
  ```
  docker run -d nginx
  ```

- To run in interactive mode (get a shell prompt inside the container):
  ```
  docker run -it ubuntu
  ```
### What is Interactive Mode in Docker?

If you want to run a container in interactive mode (with a terminal session), use the `-it` option with `docker run`:

```
docker run -it <image_name>
```

- `-i` (interactive): Keeps STDIN open so you can interact with the container.
- `-t` (tty): Allocates a pseudo-TTY (terminal).

**Example:**
```
docker run -it ubuntu
```
This command starts an Ubuntu container and gives you a shell prompt inside the container.


- To run and open a Bash shell in the container:
  ```
  docker run -it ubuntu bash
  ```

- To run and open a sh shell in the container:
  ```
  docker run -it alpine sh
  ```

- To run a container and map a port (host:container):
  ```
  docker run -p 8080:80 nginx
  ```
  (This maps port 80 in the container to port 8080 on your host.)

- To assign a name to your container:
  ```
  docker run --name mynginx nginx
  ```

- To remove a container after it exits:
  ```
  docker run --rm ubuntu
  ```

### List All Images

```
docker images
```

### List Running Containers

```
docker ps
```

### List All Containers (active and inactive)

```
docker ps -a
```

### Start/Stop/Remove Containers

- Start a stopped container:
  ```
  docker start <container_id or name>
  ```
- Stop a running container:
  ```
  docker stop <container_id or name>
  ```
- Remove a container:
  ```
  docker rm <container_id or name>
  ```

### Attach to a Running Container

- Attach to a running container's main process:
  ```
  docker attach <container_id or name>
  ```

- Open a new shell session in a running container:
  ```
  docker exec -it <container_id or name> bash
  ```
  (Use `sh` instead of `bash` if bash is not available.)

### Remove an Image

```
docker rmi <image_id>
```



**Detached Mode:**  
- The container runs in the background, and you get back your terminal prompt immediately.
- Useful for running services (like web servers) that should keep running.

**Attached Mode:**  
- The container runs in the foreground, and you see its output in your terminal.
- You interact directly with the container process.
- Default mode if you don't use `-d`.

Example (attached mode):
```
docker run nginx
```
### Create Two Different Containers from the Same Docker Image

You can create multiple containers from the same image by running the `docker run` command multiple times. You can also assign different names to each container:

```
docker run --name container1 nginx
docker run --name container2 nginx
```

- `--name` lets you specify a unique name for each container.
- Both containers will run independently but use the same `nginx`

### Docker Networks: bridge, host, and none

When you run `docker ps -a`, you will see a "NETWORKS" column showing values like `bridge`, `host`, or `none`. These represent the network mode used by each container.

#### 1. **bridge** (default)
- Containers are connected to a private internal network on the Docker host.
- They can communicate with each other via this bridge network.
- Containers can access the outside world, but external systems must map ports to reach containers.

**Diagram:**
```
[Host OS]
   |
[Docker Bridge Network]
   |         |         |
[Cont1]  [Cont2]   [Cont3]
```

#### 2. **host**
- The container shares the host’s network stack.
- No network isolation between the container and the host.
- Useful for performance or when you need direct access to host network interfaces.

**Diagram:**
```
[Host OS Network Stack]
   |
[Container]
```

#### 3. **none**
- The container has no network access.
- No interfaces except the loopback interface (`localhost`).

**Diagram:**
```
[Container]
  (no network)
```

**Summary Table:**

| Network Mode | Description                                  | Use Case                        |
|--------------|----------------------------------------------|---------------------------------|
| bridge       | Default, isolated network for containers     | Most applications               |
| host         | Shares host network stack                    | High performance, special cases |
| none         | No network


## Dockerisizing Our App

We need to create a Dockerfile to containerize our Node.js application.
**Diagram:**
```

FROM UBUNTU [base image]

RUN apt-get update && \
    apt-get install -y curl && \
    curl -fsSL https://deb.nodesource.com/setup_18.x | bash - && \
    apt-get install -y nodejs


COPY index.js home.path/index.js
COPY packag.json home.path.package.json
COPY package-lock.josn home/path/package-lock.json

WORKING DIRECTORY hone/path
RUN npm install

CMD["npm","start"]

```


**In the terminal** 
```
docker build -t my-app .   # [build with the image name my-app (.)-> curr directory]
```
 **Layers in Docker Image**
 The lines or commands in Dockerfile are the layers. Docker caches the layers , do while building it starts from the that layer which it left because the previous layers that have been build is already cached

 **The above Dockerfile is -> 365 MB, to optimise, it we just use**
 ```
FROM node:24.9-alpine3.21

WORKING DIRECTORY hone/path

COPY packag.json package.json
COPY package-lock.josn package-lock.json

COPY index.js index.js

RUN npm install

CMD["npm","start"]
```

**Note-> that due to changes in the index.js, if index.js is at top then from the changes files again all the layers will be build again  so we write at the bottom** 
