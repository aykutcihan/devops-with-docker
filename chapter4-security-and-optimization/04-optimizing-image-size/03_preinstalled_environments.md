# Image with Preinstalled Environment

Instead of manually installing a language runtime, use a prebuilt image from Docker Hub. This is easier to maintain and keeps Dockerfiles simpler.

## Example: Python Alpine

```dockerfile
FROM python:3.12-alpine

WORKDIR /mydir

RUN apk add --no-cache curl ffmpeg ca-certificates && \
    curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o /usr/local/bin/yt-dlp && \
    chmod a+x /usr/local/bin/yt-dlp && \
    adduser -D appuser && \
    chown appuser . && \
    apk del curl

USER appuser

ENTRYPOINT ["/usr/local/bin/yt-dlp"]
```

Result: **181 MB** — slightly larger than manual Alpine install because the Python image includes more tooling, but much easier to maintain.

## Popular Preinstalled Images on Docker Hub

| Language | Image |
|----------|-------|
| Node.js | `node:20-alpine` |
| Python | `python:3.12-alpine` |
| Go | `golang:1.21-alpine` |
| Ruby | `ruby:3-alpine` |
| Java | `eclipse-temurin:21-alpine` |

Always check if an Alpine variant exists — it gives you the runtime without the Ubuntu overhead.

## Publishing Multiple Variants

```bash
docker image tag yt-dlp:alpine-3.21 <username>/yt-dlp:alpine-3.21
docker image push <username>/yt-dlp:alpine-3.21

docker image tag yt-dlp:python-alpine <username>/yt-dlp:python-alpine
docker image push <username>/yt-dlp:python-alpine
```

`:latest` refers to whatever was most recently pushed — not necessarily the most stable version.
