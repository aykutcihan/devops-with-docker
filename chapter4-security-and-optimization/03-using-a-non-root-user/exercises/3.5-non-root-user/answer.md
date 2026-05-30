# Exercise 3.5 - Non-Root User

## Frontend Dockerfile

```dockerfile
FROM ubuntu:22.04

WORKDIR /usr/src/app

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_16.x | bash
RUN apt-get install -y nodejs

COPY . .

RUN npm install
RUN npm run build
RUN npm install -g serve

RUN useradd -m appuser
USER appuser

EXPOSE 5001

CMD ["serve", "-s", "-l", "5001", "build"]
```

## Backend Dockerfile

```dockerfile
FROM golang:1.16

WORKDIR /usr/src/app

COPY . .

RUN go build

RUN useradd -m appuser
USER appuser

EXPOSE 8080

CMD ["./server"]
```

## Notes

- `useradd -m appuser` creates the user before switching to it
- `USER appuser` switches all subsequent instructions and the container process to non-root
- Both apps use ports >= 1024 so no privilege issues
- Packages installed before `USER` switch (requires root)
