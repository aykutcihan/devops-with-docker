# Exercise 2.11 - Answer

## What was done

Containerized the example frontend and backend projects from the course material. Added Dockerfiles to both, then connected them with docker-compose.yaml including a Redis cache and PostgreSQL database.

The setup allows running the full stack with a single `docker compose up` command without installing Node.js, Go, or any database on the host machine.

## docker-compose.yaml

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
