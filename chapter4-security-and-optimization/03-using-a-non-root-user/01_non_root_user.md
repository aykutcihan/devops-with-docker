# Using a Non-Root User

## Why Non-Root Matters

By default, processes inside Docker containers run as **root**. This is a security risk:

- If the container is compromised, the attacker has root-level access inside the container
- With certain misconfigurations (e.g., bind mounts), root inside the container can map to root on the host
- The principle of least privilege: give processes only the permissions they need

## Creating a Non-Root User in Dockerfile

```dockerfile
FROM ubuntu:22.04

# Create a user and group
RUN groupadd -r appgroup && useradd -r -g appgroup appuser

WORKDIR /app
COPY . .

# Switch to non-root user
USER appuser

CMD ["./start.sh"]
```

## Key Instructions

- `RUN groupadd / useradd` — create the user before switching to it
- `USER` — sets the user for subsequent `RUN`, `CMD`, `ENTRYPOINT` instructions
- Files copied before `USER` are owned by root — use `chown` if the app needs write access

## Handling File Permissions

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

## Alpine-Based Images

Alpine Linux uses `addgroup` and `adduser` instead:

```dockerfile
FROM alpine:3.19

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

USER appuser
```

## Verifying the User

```bash
docker run myimage whoami
# appuser
```

## Common Pitfalls

| Issue | Cause | Fix |
|-------|-------|-----|
| Permission denied on files | Files owned by root | Use `COPY --chown` or `RUN chown` |
| Can't bind to port < 1024 | Non-root can't use privileged ports | Use port >= 1024, or use a reverse proxy |
| Package install fails | `apt install` requires root | Install packages before `USER` switch |

## Port Restriction

Ports below 1024 require root. If your app needs port 80:

```dockerfile
# Wrong: switch to non-root before binding port 80
# Right: expose a high port internally, use nginx/reverse proxy for 80

EXPOSE 3000
USER appuser
CMD ["node", "index.js"]
```

Use a reverse proxy (nginx) or load balancer to handle port 80/443 externally.
