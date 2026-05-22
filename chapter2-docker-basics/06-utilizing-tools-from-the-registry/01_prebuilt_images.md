# Utilizing Tools from the Registry

## Prebuilt Images

Instead of starting from a plain base image like `ubuntu` and manually installing everything, you can use prebuilt images that already have a language runtime installed.

Examples:
- `ruby:3.1.0` → Ruby already installed
- `golang:1.16` → Go already installed
- `amazoncorretto:8` → Java 8 already installed
- `python:3.11` → Python already installed

This simplifies Dockerfiles significantly — no need to manually install the language runtime.

## Publishing to Docker Hub

1. Create an account at hub.docker.com
2. Create a repository
3. Tag your image with your username:

```bash
docker tag <image> <username>/<repository>
```

4. Login and push:

```bash
docker login
docker push <username>/<repository>
```

Anyone can now pull and run your image:

```bash
docker pull aykutcihan/yt-dlp
docker run aykutcihan/yt-dlp https://youtube.com/...
```
