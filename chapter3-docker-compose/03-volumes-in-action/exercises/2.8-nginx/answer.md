# Exercise 2.8 - Answer

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

## nginx.conf

```nginx
events { worker_connections 1024; }

http {
  server {
    listen 80;

    location / {
      proxy_pass http://frontend:5001;
    }

    location /api/ {
      proxy_set_header Host $host;
      proxy_pass http://backend:8080;
    }
  }
}
```

## Notes

- Only `nginx` has `ports:` — frontend and backend are not directly reachable from the host
- `location /` routes to frontend, `location /api/` routes to backend
- Service names used as hostnames thanks to Docker internal DNS
