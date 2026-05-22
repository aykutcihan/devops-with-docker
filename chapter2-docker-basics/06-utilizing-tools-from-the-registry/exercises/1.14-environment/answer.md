# Exercise 1.14 - Environment

## Frontend Dockerfile

```dockerfile
FROM ubuntu:22.04

WORKDIR /usr/src/app

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_16.x | bash
RUN apt-get install -y nodejs

COPY . .

RUN npm install

ENV REACT_APP_BACKEND_URL=http://localhost:8080

RUN npm run build
RUN npm install -g serve

EXPOSE 5001

CMD ["serve", "-s", "-l", "5001", "build"]
```

## Backend Dockerfile

```dockerfile
FROM golang:1.16

EXPOSE 8080

WORKDIR /usr/src/app

COPY . .

RUN go build

ENV REQUEST_ORIGIN=http://localhost:5001

CMD ["./server"]
```

## Commands

```bash
# Backend
docker build -t backend .
docker run -d -p 8080:8080 backend

# Frontend
docker build -t frontend .
docker run -d -p 5001:5001 frontend
```

## Notes

- `REACT_APP_BACKEND_URL` → tells frontend where the backend is (set before npm run build)
- `REQUEST_ORIGIN` → tells backend to allow CORS requests from frontend
