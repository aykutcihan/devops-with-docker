# Exercise 1.5 - Sizes of Images

## Commands Used

```bash
docker pull devopsdockeruh/simple-web-service:alpine
docker pull devopsdockeruh/simple-web-service:ubuntu
docker image ls | findstr simple-web-service
```

## Image Sizes

- **alpine**: 24.3 MB
- **ubuntu**: 126 MB

## Secret Message (Alpine)

```bash
docker run -d devopsdockeruh/simple-web-service:alpine
docker exec -it <container_id> sh
tail -f ./text.log
```

Secret message is: `You can find the source code here: https://github.com/docker-hy`
