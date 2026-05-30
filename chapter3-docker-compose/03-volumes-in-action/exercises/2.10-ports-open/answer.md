# Exercise 2.10 - Answer

## Verification Command

```bash
docker run -it --rm --network host networkstatic/nmap localhost
```

## Expected Result

Only port 8000 (Nginx) is open. Ports 5001 (frontend) and 8080 (backend) are not exposed.

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

## Notes

- Only `nginx` has `ports:` defined — all other services are internal only
- Frontend and backend are unreachable directly from the host network
