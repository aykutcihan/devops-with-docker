# Exercise 3.7 - Project with Preinstalled Environments

## Image Sizes Before (from exercise 3.6)

| Image | Size |
|-------|------|
| example-frontend | 1.06 GB |
| example-backend | 1.47 GB |

## Frontend Dockerfile (node:16-alpine)

```dockerfile
FROM node:16-alpine

WORKDIR /usr/src/app

COPY . .

RUN npm install && \
    npm run build && \
    npm install -g serve && \
    rm -rf src/

RUN adduser -D appuser
USER appuser

ENV REACT_APP_BACKEND_URL=http://localhost:8080

EXPOSE 5001

CMD ["serve", "-s", "-l", "5001", "build"]
```

## Backend Dockerfile (golang:1.16-alpine)

```dockerfile
FROM golang:1.16-alpine

EXPOSE 8080

WORKDIR /usr/src/app

COPY . .

RUN go build && \
    rm -rf /root/.cache/go-build

RUN adduser -D appuser
USER appuser

ENV REQUEST_ORIGIN=http://localhost:5001

CMD ["./server"]
```

## Image Sizes After

| Image | Before | After |
|-------|--------|-------|
| example-frontend | 1.06 GB | 949 MB |
| example-backend | 1.47 GB | 580 MB |
