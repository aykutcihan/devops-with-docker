# Exercise 1.8 - Two Line Dockerfile

## i) Dockerfile

```dockerfile
FROM devopsdockeruh/simple-web-service:alpine

CMD ["server"]
```

## ii) Commands

```bash
docker build -t web-server .
docker run web-server
```

## Result

```
[GIN-debug] Listening and serving HTTP on :8080
```
