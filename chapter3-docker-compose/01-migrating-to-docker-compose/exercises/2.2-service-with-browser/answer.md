# Exercise 2.2 - Simple service with browser

## docker-compose.yaml

```yaml
services:
  simple-web-service:
    image: devopsdockeruh/simple-web-service
    ports:
      - "8080:8080"
    command: server
```

## Notes

- `command: server` switches the container from log mode to web server mode
- `ports` publishes port 8080 so the browser can reach it
- After `docker compose up`, open http://localhost:8080 in the browser
