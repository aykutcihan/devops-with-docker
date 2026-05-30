# Multi-Stage Builds

Use when you need tools for building but not for running the application. The final image only contains what you explicitly copy into it.

## Jekyll + Nginx Example

```dockerfile
# Stage 1: Build
FROM ruby:3 AS build-stage
WORKDIR /usr/app

RUN gem install jekyll
RUN jekyll new .
RUN jekyll build

# Stage 2: Serve
FROM nginx:1.19-alpine

COPY --from=build-stage /usr/app/_site/ /usr/share/nginx/html
```

Result:
- `jekyll:ruby` → **1.57 GB**
- `jekyll:nginx` → **35.3 MB**

`COPY --from=build-stage` copies files from the named stage into the current stage. You can also copy from an external image: `--from=python:3.12`.

## FROM scratch

The most minimal base — a completely empty image. Only works for statically compiled binaries.

```dockerfile
FROM golang:1.21 AS build
WORKDIR /app
COPY . .
RUN CGO_ENABLED=0 go build -o server .

FROM scratch
COPY --from=build /app/server /server
EXPOSE 8080
ENTRYPOINT ["/server"]
```

`CGO_ENABLED=0` disables cgo so the binary is fully static and can run on scratch.

## Size Progression Summary

| Technique | Size |
|-----------|------|
| Ubuntu, multiple RUN | 869 MB |
| Ubuntu, combined RUN | 866 MB |
| Ubuntu, cleaned apt | 807 MB |
| Ubuntu, removed curl | 803 MB |
| Alpine | 176 MB |
| Multi-stage (nginx) | 35.3 MB |
| FROM scratch (binary only) | ~10 MB |
