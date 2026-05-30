# Exercise 3.6 - Optimized Project Images

## Image Sizes Before Optimization

| Image | Size |
|-------|------|
| example-frontend | 1.19 GB |
| example-backend | 1.54 GB |

## Optimized Frontend Dockerfile

Ubuntu base, joined RUN commands, removed `src/` after build, cleaned apt lists, added non-root user.

```dockerfile
FROM ubuntu:22.04

WORKDIR /usr/src/app

RUN apt-get update && apt-get install -y curl && \
    curl -sL https://deb.nodesource.com/setup_16.x | bash && \
    apt-get install -y nodejs && \
    rm -rf /var/lib/apt/lists/*

COPY . .

RUN npm install && \
    npm run build && \
    npm install -g serve && \
    rm -rf src/

RUN useradd -m appuser
USER appuser

ENV REACT_APP_BACKEND_URL=http://localhost:8080

EXPOSE 5001

CMD ["serve", "-s", "-l", "5001", "build"]
```

## Optimized Backend Dockerfile

Golang base, removed go build cache after build, added non-root user.

```dockerfile
FROM golang:1.16

EXPOSE 8080

WORKDIR /usr/src/app

COPY . .

RUN go build && \
    rm -rf /root/.cache/go-build

RUN useradd -m appuser
USER appuser

ENV REQUEST_ORIGIN=http://localhost:5001

CMD ["./server"]
```

## Image Sizes After Optimization

| Image | Before | After |
|-------|--------|-------|
| example-frontend | 1.19 GB | 1.06 GB |
| example-backend | 1.54 GB | 1.47 GB |
