# Exercise 2.7 - Answer

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
    volumes:
      - ./database:/var/lib/postgresql/data
    restart: unless-stopped
```

## Notes

- `./database` bind mount replaces the anonymous volume from Exercise 2.6
- Data persists across `docker compose down` as long as the `./database` folder is not deleted
- Delete the folder manually to verify data is gone after restart
