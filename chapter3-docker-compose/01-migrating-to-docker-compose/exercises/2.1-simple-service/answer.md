# Exercise 2.1 - Answer

## docker-compose.yaml

```yaml
services:
  simple-web-service:
    image: devopsdockeruh/simple-web-service
    volumes:
      - ./text.log:/usr/src/app/text.log
```

## Notes

- `text.log` must exist on the host before running, otherwise Docker creates it as a directory
- The service writes logs into the file via the bind mount
