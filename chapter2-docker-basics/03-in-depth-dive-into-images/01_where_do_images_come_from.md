# Where Do Images Come From?

## Docker Hub

Docker Hub is the default public registry where images are stored and shared. When you run `docker run hello-world`, Docker first checks locally — if not found, it pulls from Docker Hub automatically.

You can search for images from the command line:

```bash
docker search hello-world
```

## Official vs Community Images

- **Official images** → curated and reviewed by Docker. No prefix in the name (e.g. `ubuntu`, `nginx`, `postgres`). Marked with `[OK]` in the OFFICIAL column.
- **Community images** → published by anyone. Named as `username/image` (e.g. `devopsdockeruh/simple-web-service`).

## Other Registries

Docker Hub is the default, but other registries exist (e.g. Quay). To pull from a different registry, include the host:

```bash
docker pull quay.io/podman/hello
```

If no host is specified, Docker defaults to Docker Hub.

## Image Name Structure

An image name can have up to 3 parts plus a tag:

```
registry/organisation/image:tag
```

- `ubuntu` → registry=Docker Hub, organisation=library, tag=latest
- `ubuntu:25.10` → specific version
- `devopsdockeruh/simple-web-service:ubuntu` → community image with tag
