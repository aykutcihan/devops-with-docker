# Optimizing Image Size

## Why Image Size Matters

- Smaller images pull faster (especially in CI/CD)
- Less surface area for security vulnerabilities
- Lower storage costs on registries
- Faster container startup

## Layer Caching

Every `RUN`, `COPY`, `ADD` creates a new layer. Layers are cached — if nothing changes, Docker reuses the cached layer.

```dockerfile
# Bad: changes to source code invalidate npm install cache
COPY . .
RUN npm install

# Good: dependencies cached separately from source changes
COPY package*.json .
RUN npm install
COPY . .
```

## Multi-Stage Builds

The most powerful optimization. Build artifacts in one stage, copy only what's needed to the final image.

```dockerfile
# Stage 1: Build
FROM node:20 AS build
WORKDIR /app
COPY package*.json .
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Production
FROM node:20-alpine
WORKDIR /app
COPY --from=build /app/dist ./dist
COPY --from=build /app/node_modules ./node_modules
EXPOSE 3000
CMD ["node", "dist/index.js"]
```

The final image only contains the runtime artifacts — not the build tools, dev dependencies, or source code.

### Multi-Stage for Go

```dockerfile
FROM golang:1.21 AS build
WORKDIR /app
COPY . .
RUN go build -o server .

FROM scratch
COPY --from=build /app/server /server
EXPOSE 8080
ENTRYPOINT ["/server"]
```

`FROM scratch` is an empty image — the resulting image is just the binary.

## Choosing the Right Base Image

| Base | Size | Use Case |
|------|------|----------|
| `ubuntu:22.04` | ~77MB | General purpose |
| `debian:slim` | ~30MB | Smaller Debian |
| `alpine:3.19` | ~7MB | Minimal, musl libc |
| `scratch` | 0MB | Static binaries only |
| `distroless` | ~2-20MB | No shell, security-focused |

### Alpine Considerations

Alpine uses musl libc instead of glibc. Most apps work fine, but some compiled binaries may not.

## Minimizing Layers

Combine related `RUN` commands:

```dockerfile
# Bad: 3 layers
RUN apt-get update
RUN apt-get install -y curl
RUN rm -rf /var/lib/apt/lists/*

# Good: 1 layer
RUN apt-get update && \
    apt-get install -y curl && \
    rm -rf /var/lib/apt/lists/*
```

Always clean up package manager caches in the same `RUN` command — cleanup in a separate layer doesn't reduce size.

## .dockerignore

Prevent unnecessary files from being sent to the build context:

```
node_modules
.git
*.log
.env
dist
coverage
README.md
```

## Checking Image Size

```bash
docker images
docker image inspect myimage --format='{{.Size}}'

# Dive tool — analyze layer by layer
docker run --rm -it \
  -v /var/run/docker.sock:/var/run/docker.sock \
  wagoodman/dive myimage
```

## Summary

| Technique | Impact |
|-----------|--------|
| Multi-stage builds | Largest reduction — removes build tools |
| Alpine base image | 70-90% smaller than ubuntu |
| Combine RUN commands | Fewer layers, smaller size |
| .dockerignore | Smaller build context |
| Layer ordering | Better cache utilization |
