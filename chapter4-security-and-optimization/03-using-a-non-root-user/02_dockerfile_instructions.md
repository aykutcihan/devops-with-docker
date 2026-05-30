# Dockerfile Instructions for Non-Root User

## Ubuntu / Debian

```dockerfile
FROM ubuntu:22.04

RUN groupadd -r appgroup && useradd -r -g appgroup appuser

WORKDIR /app
COPY . .

USER appuser

CMD ["./start.sh"]
```

- `RUN groupadd / useradd` — create the user before switching to it
- `USER` — sets the user for subsequent `RUN`, `CMD`, `ENTRYPOINT` instructions
- Files copied before `USER` are owned by root — use `chown` if the app needs write access

## Alpine

Alpine uses `addgroup` and `adduser` instead of `groupadd` / `useradd`:

```dockerfile
FROM alpine:3.19

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

USER appuser
```

## File Permissions with COPY --chown

```dockerfile
FROM node:20

RUN groupadd -r appgroup && useradd -r -g appgroup appuser

WORKDIR /app
COPY --chown=appuser:appgroup . .

RUN npm install

USER appuser

CMD ["node", "index.js"]
```

`COPY --chown` sets ownership at copy time, avoiding a separate `RUN chown` layer.

## Common Pitfalls

| Issue | Cause | Fix |
|-------|-------|-----|
| Permission denied on files | Files owned by root | Use `COPY --chown` or `RUN chown` |
| Can't bind to port < 1024 | Non-root can't use privileged ports | Use port >= 1024 or a reverse proxy |
| Package install fails | `apt install` requires root | Install packages before `USER` switch |

## Port Restriction

Ports below 1024 require root. Use a high port internally and a reverse proxy for port 80/443:

```dockerfile
EXPOSE 3000
USER appuser
CMD ["node", "index.js"]
```
