# Exercise 2.6 - Answer

## docker-compose.yaml

```yaml
services:
  frontend:
    image: frontend
    ports:
      - "5001:5001"

  backend:
    image: backend
    ports:
      - "8080:8080"
    environment:
      - REQUEST_ORIGIN=http://localhost:5001
      - REDIS_HOST=redis
      - POSTGRES_HOST=db
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
      - POSTGRES_DATABASE=postgres
    restart: unless-stopped

  redis:
    image: redis

  db:
    image: postgres:13.2-alpine
    environment:
      - POSTGRES_PASSWORD=postgres
    restart: unless-stopped
```

## Notes

- `POSTGRES_HOST=db` — backend connects to Postgres using the service name
- `db` has no `ports:` — only accessible internally
- No volume defined — Postgres creates an anonymous volume automatically (sufficient for this exercise)
- `restart: unless-stopped` — backend retries until Postgres is ready
