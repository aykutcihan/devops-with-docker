# Docker CLI Basics

## Docker Engine Components
Docker Engine consists of 3 parts:
1. **CLI client** — the commands you type in the terminal
2. **REST API** — the bridge between CLI and daemon
3. **Docker daemon** — the service that does the actual work (manages images, containers, resources)

When you run a command, the CLI sends a request to the daemon via REST API, and the daemon executes it.

## Key Rules

### Removing an Image
You cannot remove an image if a container created from it still exists — even if that container is stopped. You must remove the container first, then the image.

```bash
docker container rm <id or name>
docker image rm <image>
```

### Removing a Running Container
You cannot remove a running container directly. You must stop it first.

```bash
docker container stop <name>
docker container rm <name>
```

## Useful Commands

```bash
# Run container in detached mode (background)
docker run -d nginx

# List running containers
docker ps

# List all containers including stopped ones
docker ps -a

# Filter containers (Linux/Mac)
docker container ls -a | grep hello-world

# Filter containers (Windows PowerShell)
docker container ls -a | findstr hello-world

# Remove multiple containers at once
docker container rm id1 id2 id3

# Remove all stopped containers
docker container prune

# Remove dangling images
docker image prune

# Remove almost everything
docker system prune

# Pull image without running
docker image pull hello-world
```

## Detached Mode (-d flag)
Without `-d`: terminal freezes, container runs in the foreground. Use `Ctrl+C` to exit.  
With `-d`: container runs in the background, terminal stays free.

## Container ID Shorthand
You don't need to type the full container ID. The first few characters are enough as long as they are unique.
```bash
docker container rm 3d   # works if only one ID starts with "3d"
```
