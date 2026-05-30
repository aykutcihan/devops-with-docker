# Exercise 3.9 - Multi-Stage Backend

## Dockerfile

```dockerfile
FROM golang:1.16-alpine AS build-stage
WORKDIR /usr/src/app
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o server .

FROM scratch
COPY --from=build-stage /usr/src/app/server /server
EXPOSE 8080
CMD ["/server"]
```

## Result

| Tag | Size |
|-----|------|
| 3.7 (golang:1.16-alpine) | 580 MB |
| 3.9 (multi-stage + scratch) | 26.7 MB |

`CGO_ENABLED=0` disables cgo so the binary is fully statically linked and can run in `FROM scratch` (which has no libc or any system libraries). `GOOS=linux` ensures the binary targets Linux regardless of the build machine OS.
