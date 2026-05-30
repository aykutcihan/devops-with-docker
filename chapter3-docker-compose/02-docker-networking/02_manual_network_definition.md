# Manual Network Definition

Networks can be defined manually in `docker-compose.yaml`. This is useful when containers from **two different compose files** need to share the same network.

## Defining a Network

```yaml
services:
  db:
    image: postgres:18.1-alpine
    networks:
      - database-network

networks:
  database-network:
    name: the-database-network
```

Created with `docker compose up`, removed with `docker compose down`.

## Connecting to an External Network

```yaml
services:
  db:
    image: backend-image
    networks:
      - database-network

networks:
  database-network:
    external:
      name: the-database-network  # must match the actual network name
```

## Default Network Override

```yaml
services:
  db:
    image: backend-image

networks:
  default:
    external:
      name: the-database-network
```

All services automatically join the external network without needing explicit `networks:` per service.
