# docker-compose.yaml Syntax

## Basic Structure

```yaml
services:
  service-name:
    image: image-name
    build: ./path/to/dockerfile
    ports:
      - "host_port:container_port"
    volumes:
      - ./host/path:/container/path
    environment:
      - ENV_VAR=value
    depends_on:
      - other-service
```

## Key Fields

| Field | Purpose |
|-------|---------|
| `services` | Top-level key — lists all containers |
| `image` | Use an existing image from registry |
| `build` | Build from a local Dockerfile |
| `ports` | Port mapping (host:container) |
| `volumes` | Bind mounts or named volumes |
| `environment` | Set environment variables |
| `depends_on` | Start order: wait for another service |
