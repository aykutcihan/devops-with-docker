# Networking in Compose

All services in a `docker-compose.yaml` are automatically placed on the same network. No manual `--network` flags needed.

## Service Discovery by Name

Services reach each other using their **service name** as hostname.

```yaml
services:
  backend:
    image: mybackend

  db:
    image: postgres
```

The `backend` container can connect to the database at `db:5432` — Docker resolves `db` to the right container IP automatically.

## Comparison with docker run

| docker run | docker compose |
|-----------|---------------|
| `--network mynet` on every container | automatic shared network |
| use container IP or --link | use service name as hostname |
| manual network creation | nothing needed |
