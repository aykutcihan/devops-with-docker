# Named vs Anonymous Volumes

## Anonymous Volumes

Created automatically by Docker when an image declares a `VOLUME` instruction in its Dockerfile. Docker gives them a random ID — hard to track and manage.

```bash
docker volume ls
# DRIVER    VOLUME NAME
# local     a3f2e1b...  ← anonymous, hard to identify
```

## Named Volumes

Explicitly defined in `docker-compose.yaml`. Human-readable name, easy to inspect and reuse.

```yaml
services:
  db:
    image: postgres:13.2-alpine
    volumes:
      - database:/var/lib/postgresql/data   # named volume

volumes:
  database:                                 # declared at bottom
```

Docker creates a volume named `<project>_database` instead of a random ID.

## Bind Mounts

Maps a specific host directory into the container. Useful for development and backups.

```yaml
volumes:
  - ./database:/var/lib/postgresql/data    # host path : container path
```

| Type | Host path | Managed by | Use case |
|------|-----------|-----------|---------|
| Anonymous | random | Docker | quick temp data |
| Named | Docker area | Docker | persistent app data |
| Bind mount | your choice | you | dev, backups |
