# Watchtower

Watchtower monitors Docker Hub and automatically pulls and restarts containers when a new image is available.

## docker-compose.yaml

```yaml
services:
  watchtower:
    image: containrrr/watchtower
    environment:
      - WATCHTOWER_POLL_INTERVAL=60
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    container_name: watchtower
```

## How it works

- `WATCHTOWER_POLL_INTERVAL=60` → checks Docker Hub every 60 seconds
- `/var/run/docker.sock` → mounts the Docker socket so Watchtower can manage other containers on the host
- When a new image is found, Watchtower pulls it and restarts the container automatically

## docker.sock

The Docker socket is how the Docker CLI talks to the Docker daemon. Mounting it into a container gives that container full control over Docker on the host — including starting, stopping, and pulling containers.
