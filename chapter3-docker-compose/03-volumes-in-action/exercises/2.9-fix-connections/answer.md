# Exercise 2.9 - Answer

## Changes Made

`REACT_APP_BACKEND_URL` was baked into the frontend image as `http://localhost:8080` at build time. After adding Nginx, the backend is no longer directly accessible on port 8080 — all traffic goes through `http://localhost:8000`. The frontend needed to be rebuilt with the correct URL.

### Frontend Dockerfile change

```dockerfile
ENV REACT_APP_BACKEND_URL=http://localhost:8000
```

### Rebuild frontend

```bash
docker build -t frontend .
```

### docker-compose.yaml (same as 2.8)

```yaml
services:
  frontend:
    image: frontend

  backend:
    image: backend
    environment:
      - REQUEST_ORIGIN=http://localhost:8000
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
    volumes:
      - ./database:/var/lib/postgresql/data
    restart: unless-stopped

  nginx:
    image: nginx
    ports:
      - "8000:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
```
