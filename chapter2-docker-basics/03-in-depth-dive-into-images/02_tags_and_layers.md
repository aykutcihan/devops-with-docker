# Tags and Layers

## Tags

A tag defines the version of an image. You add it after the image name with a colon:

```bash
docker pull ubuntu          # pulls ubuntu:latest by default
docker pull ubuntu:25.10    # pulls specific version
```

- `latest` is the default tag when none is specified
- Using specific tags in production is safer — `latest` can change unexpectedly

You can also create local tags:

```bash
docker tag ubuntu:25.10 ubuntu:questing_quokka
```

## Layers

Images are not single files — they are made of multiple layers stacked on top of each other. Each instruction in a Dockerfile creates a new layer.

When pulling an image, each layer is downloaded separately:

```
16c195d4c5e9: Pull complete
458996317100: Pull complete
```

### Why layers matter

- **Cache**: If a layer hasn't changed, Docker reuses it from cache during build — faster builds
- **Sharing**: If two images share a layer, Docker stores it only once — saves disk space

Example: `ubuntu:latest` and `ubuntu:25.10` share many layers. Those shared layers are downloaded only once.
