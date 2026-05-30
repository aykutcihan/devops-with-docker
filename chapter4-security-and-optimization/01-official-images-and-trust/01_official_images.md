# Official Images and Trust

## What makes an image "official"?

Docker Official Images are maintained by the [Docker Official Images](https://github.com/docker-library/official-images) organization. They are added via a pull request process and verified by maintainers. Being "official" doesn't mean they are inherently safer — it means the build process is open and auditable.

Well-known official images include `postgres`, `python`, `ubuntu`, `node`.

## Verifying an Image

You can trace exactly where an image comes from:

1. Check the Docker Hub page — it links to the source Dockerfile
2. Use `docker image history` to see the build layers:

```bash
docker image history --no-trunc ubuntu:22.04
```

The output should match the instructions in the source Dockerfile. If they match, you can trust the image is what it claims to be.

## FROM scratch

The most minimal possible base. `scratch` is a special empty image — nothing in it. When Ubuntu's Dockerfile starts with `FROM scratch`, it adds a compressed tarball of the OS root filesystem:

```dockerfile
FROM scratch
ADD ubuntu-*-oci-amd64-root.tar.gz /
```

The `ADD` instruction automatically extracts tar archives — so this single line creates the entire base OS layer.

## Key Takeaway

> "You can't trust code that you did not totally create yourself."
> — Ken Thompson (1984, Reflections on Trusting Trust)

There is nothing magical about official images. The build processes are open — you can audit them, verify checksums, or even build the image yourself if needed.
