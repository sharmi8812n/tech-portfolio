# Docker – Overview & Basics

## What is Docker?

Docker is an open-source platform that automates the building, shipping, and running of applications inside lightweight, portable containers. Containers package an application and its dependencies together, enabling consistent environments across development, testing, and production.

---

## Key Concepts

- **Image:** A read-only template with instructions for creating a container (like a snapshot of an app).  
- **Container:** A runnable instance of an image. It includes the app and its environment.  
- **Dockerfile:** A text file with commands to build a Docker image.  
- **Docker Hub:** A public registry to store and share Docker images.  
- **Volumes:** Persistent storage for containers.  

---

## How Docker Works

1. **Write Dockerfile:** Define how to build your application image.  
2. **Build Image:** Use `docker build` to create an image from Dockerfile.  
3. **Run Container:** Use `docker run` to start a container from an image.  
4. **Manage Containers:** Start, stop, remove, and inspect running containers.  
5. **Share Images:** Push images to Docker Hub or private registries.

---

## Common Docker Commands

### Working with Images
- `docker build -t <image-name> .`  
  Build image from Dockerfile in current directory.

- `docker pull <image>`  
  Download image from Docker Hub.

- `docker images`  
  List local images.

- `docker rmi <image-id>`  
  Remove an image.

### Working with Containers
- `docker run -d --name <container-name> -p 80:80 <image>`  
  Run container in detached mode and map port 80.

- `docker ps`  
  List running containers.

- `docker ps -a`  
  List all containers (running + stopped).

- `docker stop <container-id>`  
  Stop a running container.

- `docker start <container-id>`  
  Start a stopped container.

- `docker rm <container-id>`  
  Remove a container.

- `docker logs <container-id>`  
  View logs of a container.

- `docker exec -it <container-id> /bin/bash`  
  Open an interactive shell inside a running container.

### Volumes & Networking
- `docker volume create <volume-name>`  
  Create a volume.

- `docker run -v <volume-name>:/data ...`  
  Mount volume inside container.

- `docker network ls`  
  List networks.

---

## Sample Dockerfile

```dockerfile
# Use official Node.js runtime as a parent image
FROM node:14

# Set working directory
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy app source code
COPY . .

# Expose port
EXPOSE 3000

# Start the app
CMD ["node", "server.js"]
