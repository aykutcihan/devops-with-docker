# Exercise 1.13 - Hello Backend

## Dockerfile

```dockerfile
FROM golang:1.16

EXPOSE 8080

WORKDIR /usr/src/app

COPY . .

RUN go build

CMD ["./server"]
```

## Commands

```bash
docker build -t backend .
docker run -p 8080:8080 backend
```
