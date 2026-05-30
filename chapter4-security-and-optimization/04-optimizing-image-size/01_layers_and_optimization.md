# Layers and Optimization

## Video

[Building Small Containers - Google](https://www.youtube.com/watch?v=wGz_cbtCiEA)

## Why Image Size Matters

- Smaller images pull faster (especially in CI/CD)
- Less surface area for security vulnerabilities
- Lower storage costs on registries
- Faster container startup

## What Is a Layer?

Every instruction in a Dockerfile creates a layer in the image. When you change the Dockerfile and rebuild, only changed layers are rebuilt — this is what makes images lightweight and fast.

## Reducing Layers

### Starting point: 869 MB

```dockerfile
FROM ubuntu:24.04

WORKDIR /mydir

RUN apt-get update && apt-get install -y curl python3 ffmpeg
RUN curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o /usr/local/bin/yt-dlp
RUN chmod a+x /usr/local/bin/yt-dlp

RUN useradd -m appuser
RUN chown appuser .

USER appuser

ENTRYPOINT ["/usr/local/bin/yt-dlp"]
```

### Combine RUN commands: 866 MB

```dockerfile
FROM ubuntu:24.04

WORKDIR /mydir

RUN apt-get update && apt-get install -y curl python3 ffmpeg && \
    curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o /usr/local/bin/yt-dlp && \
    chmod a+x /usr/local/bin/yt-dlp && \
    useradd -m appuser && \
    chown appuser .

USER appuser

ENTRYPOINT ["/usr/local/bin/yt-dlp"]
```

Only 3 MB smaller — the real gains come from cleanup.

### Remove apt lists: 807 MB

```dockerfile
.. && \
rm -rf /var/lib/apt/lists/*
```

### Remove curl after use: 803 MB

```dockerfile
.. && \
apt-get purge -y --auto-remove curl && \
rm -rf /var/lib/apt/lists/*
```

Always clean up in the **same RUN command** — a separate `RUN rm` creates a new layer and does not reduce the image size.

## Inspecting Layers

```bash
docker image history yt-dlp
```

Example output:

```
IMAGE          CREATED          CREATED BY                                      SIZE
731a086e8f41   52 seconds ago   ENTRYPOINT ["/usr/local/bin/yt-dlp"]            0B
<missing>      52 seconds ago   USER appuser                                    0B
<missing>      52 seconds ago   RUN /bin/sh -c apt-get update && apt-get ins…   788MB
```
