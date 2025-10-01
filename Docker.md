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

## Expose Port

**Port Binding**
```
docker run -it -p 8080:80 <image_id>   # this is the bonding of the host port to that of the container port 
```
Disadvantage : When binding host ports, conflicts may occur if the port is already in use.

For example, if another service is running on port 8080, the container cannot start with the same binding.

**Exposing Port**
1. Using EXPOSE in Dockerfile makes a container port visible to the host.
2. Docker automatically binds an available host port to the exposed container port when using -P.
3. This avoids conflicts because Docker selects a free host port dynamically.

```
FROM node:24.9-alpine3.21

WORKING DIRECTORY hone/path

COPY packag.json package.json
COPY package-lock.josn package-lock.json

COPY index.js index.js

RUN npm install

EXPOSE 8080

CMD["npm","start"]
```

**In Terminal** 
```
docker run -it -d -P my-app  # -P [publishes all exposed ports to random free ports on the host]
```

## Publishing Docker Images

| Step       | Command Example                          | Purpose                          |
| ---------- | ---------------------------------------- | -------------------------------- |
| Login      | `docker login`                           | Authenticate with Docker Hub     |
| Tag Image  | `docker tag my-app ritushree/my-app:1.0` | Assign Docker Hub repo + version |
| Push Image | `docker push ritushree/my-app:1.0`       | Publish image to Docker Hub      |
| Pull Image | `docker pull ritushree/my-app:1.0`       | Download image from Docker Hub   |



**Step 1: Log in to Docker Hub**
```
docker login

```

**Step 2: Tag the Image**
```
docker tag <local_image_id> <dockerhub_username>/<repo_name>:<tag>

```
**Step 3: Push the Image**

```
docker push <dockerhub_username>/<repo_name>:<tag>
```

**Step 4: Pull the Image (Verification)**
```
docker pull <dockerhub_username>/<repo_name>:<tag>
```


## Multi-Stage Build

1. A Docker feature that allows using multiple FROM statements in a single Dockerfile.
2. Each FROM starts a new build stage.
3. Helps in creating small, optimized images by copying only the required artifacts from one stage to another.


**Advantages:**

1. Reduces final image size.
2. Keeps build tools and unnecessary files out of the production image.
3. Makes Dockerfiles cleaner and easier to manage.

```
# Stage 1: Build the application
FROM node:24.9-alpine3.21 AS builder
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install
COPY . .
RUN npm run build         # creates a dist folder

# Stage 2: Run the application
FROM node:24.9-alpine3.21
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY package.json package-lock.json ./
RUN npm install --omit=dev         # to omit all the dev dependencies in the package.json
EXPOSE 3000
CMD ["npm", "start"]
```


Explanation:

- **Stage 1 (Builder):**

1. Uses a Node.js image with build tools.
2. Installs dependencies and builds the application.
3. Produces a dist/ folder containing compiled code.

- **Stage 2 (Final Image):**

1. Starts with a fresh Node.js base image.
2. Copies only the compiled output (dist/) from the builder stage.
3. Installs only production dependencies.
4. Much smaller than including all build tools.


```
[Builder Image]
   - Node.js + Build Tools
   - Dependencies
   - Compiled App (dist/)

        |
        v

[Final Image]
   - Node.js Runtime
   - dist/ (app code)
   - Production Dependencies

```

## Add User security

**Why Add a User?**

-By default, Docker containers run processes as the root user.
-Running applications as root inside the container is risky (privilege escalation).
-Best practice: create a non-root user and run the app under that user.

```
# Stage 2: Run the application
FROM node:24.9-alpine3.21

WORKDIR /app

# Copy files from builder stage
COPY --from=builder /app/dist ./dist
COPY package.json package-lock.json ./

# Install only production dependencies
RUN npm install --omit=dev

# Create a non-root user and group
RUN addgroup --system sid 1001 nodejs


# Change ownership of the app directory
RUN adduser --system uid 1001 nodejs 

# Switch to non-root user
USER nodejs

# Expose port
ENV PORT=3000   # from the env

EXPOSE 3000

# Start the app
CMD ["npm", "start"]

```


### Docker Networks: bridge, host, and none

When you run `docker ps -a`, you will see a "NETWORKS" column showing values like `bridge`, `host`, or `none`. These represent the network mode used by each container.

#### 1. **bridge** (default)
- Containers are connected to a private internal network on the Docker host.
- They can communicate with each other via this bridge network.
- Containers can access the outside world, but external systems must map ports to reach containers.

  **2 types of bridge network**
  1. default bridge [throught IP only containers can talk]
  2. user-defined bridge [it provides the DNS method, where through naming we can talk]

```
[Container 1: 172.17.0.2]     [Container 2: 172.17.0.3]
          |                           |
          +------------+--------------+
                       |
                  +----+----+
                  | Bridge  |  (docker0: 172.17.0.1)
                  +----+----+
                       |
                       |
     +-----------------+-----------------+
     |                                   |
[ Host IP: 192.168.1.10 ]           [ Router / Internet ]
     |                                   |
     +-----------------------------------+


```
**Explanation**

- Both Host IP and Bridge (docker0) have paths leading to the Router/Internet.
- Containers talk to the outside world through the bridge → router.
- Host machine itself also directly connects to the router.

**1. Accessing Another Container via IP**

If two containers are on the same bridge network, each gets an IP (like 172.17.0.2, 172.17.0.3).
You can call one container from another using that IP:

```
# From inside Container 1, ping Container 2 by IP
docker exec -it container1 ping 172.17.0.3
```
**Why?**

-By default, Docker assigns internal IPs on the docker0 bridge.
-Containers in the same bridge can reach each other using these IPs.
-Disadvantage: IPs may change when containers restart, so not reliable.

**🔹 2. Using Container Names (Preferred)**
If you create a user-defined bridge network, containers can communicate via their names (DNS resolution) instead of IPs:

```
# Create a custom network
docker network create mynet

# Run two containers in the same network
docker run -it --name container1 --network mynet ubuntu bash
docker run -it --name container2 --network mynet ubuntu bash

# Inside container1, you can ping container2 by name
ping container2
```

**3.Connecting a Running Container to a Network**
```
docker network connect mynet container1
#container1 in another default bridge network, which i am connecting to the mynet
# so my containers at mynet can talk to the container1
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




## Docker Volumes

- Volumes are the preferred mechanism for persisting data generated and used by Docker containers.
- Unlike container layers, volumes exist outside the container’s filesystem and persist even if the container is deleted.

**🔹 Types of Volumes**

**1. Anonymous Volume**

Created automatically when a container writes to a non-existing volume path.
Not easy to manage because no name is assigned.

```
docker run -v /app/data ubuntu
```

**2. Named Volume**

Created with a custom name for easier management.
Survives container restarts and deletions.

```
docker volume create mydata
docker run -v mydata:/app/data ubuntu         #Tells Docker: Mount the volume mydata into the container’s filesystem at /app/data.
```

Note : the volume stays in the docker whether the container deletes or stays , so every container can use the volume

**3. Bind Mounts**

Maps a directory/file from the host machine into the container.
Useful for development because changes on host reflect instantly inside the container.

```
docker run -v /host/path:/container/path ubuntu         # host path: container path 
```

**🔹 Important Point**

- Data is not stored inside the container filesystem.
- Instead, the container is just mounting your host’s folder.
- So yes ✅ the container path is saved in your local system at /host/path.
- If the container is deleted, the data still remains on your local machine.



