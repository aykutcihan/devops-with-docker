# Exercise 2.4 - Answer

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
    restart: unless-stopped

  redis:
    image: redis
```

## Notes

- `REDIS_HOST=redis` — backend connects to Redis using the service name as hostname
- Redis has no `ports:` — only accessible internally within the Docker network
- `restart: unless-stopped` — backend retries if Redis isn't ready yet on startup
