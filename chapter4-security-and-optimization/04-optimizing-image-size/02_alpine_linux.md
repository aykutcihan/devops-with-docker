# Alpine Linux Variant

Alpine Linux is ~8 MB vs Ubuntu's ~77 MB. It uses `musl` libc and `busybox` — most software runs fine, but some compiled binaries may not.

## Dockerfile

```dockerfile
FROM alpine:3.21

WORKDIR /mydir

RUN apk add --no-cache curl ffmpeg python3 ca-certificates && \
    curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o /usr/local/bin/yt-dlp && \
    chmod a+x /usr/local/bin/yt-dlp && \
    adduser -D appuser && \
    chown appuser . && \
    apk del curl

USER appuser

ENTRYPOINT ["/usr/local/bin/yt-dlp"]
```

Result: **176 MB** (vs 803 MB Ubuntu)

## Building with a Tag

```bash
docker build -t yt-dlp:alpine-3.21 -f Dockerfile.alpine .
```

## Layer Size

```
IMAGE          CREATED         CREATED BY                                      SIZE
5d5ace23d52b   3 minutes ago   ENTRYPOINT ["/usr/local/bin/yt-dlp"]            0B
<missing>      3 minutes ago   USER appuser                                    0B
<missing>      3 minutes ago   RUN /bin/sh -c apk add --no-cache curl ffmpe…   168MB
```

## Alpine vs Ubuntu Differences

| Feature | Ubuntu | Alpine |
|---------|--------|--------|
| Package manager | `apt` | `apk` |
| No-cache flag | `rm -rf /var/lib/apt/lists/*` | `--no-cache` |
| Create user | `useradd -m` | `adduser -D` |
| Base size | ~77 MB | ~8 MB |

Package browser: https://pkgs.alpinelinux.org/packages
