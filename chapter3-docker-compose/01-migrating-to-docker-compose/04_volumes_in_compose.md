# Volumes in Compose

## Bind Mount (host path)

```yaml
services:
  app:
    image: myapp
    volumes:
      - ./data:/app/data
```

Maps a folder on your machine into the container. Changes on either side are reflected immediately.

## Named Volume

```yaml
services:
  app:
    image: myapp
    volumes:
      - myvolume:/app/storage

volumes:
  myvolume:
```

Named volumes are managed by Docker, not tied to a specific host path. Must be declared at the bottom under `volumes:`.

## Persistence

| Action | Bind mount | Named volume |
|--------|-----------|--------------|
| `docker compose down` | persists | persists |
| `docker compose down -v` | persists | **deleted** |
