# Building Images

## Dockerfile

A Dockerfile is a text file that contains instructions for building an image. Each instruction creates a new layer.

```dockerfile
FROM alpine:3.21          # start from this base image
WORKDIR /usr/src/app      # set working directory inside the container
COPY hello.sh .           # copy hello.sh from local machine into the image
RUN chmod +x hello.sh     # run this command during build
CMD ["./hello.sh"]        # run this when the container starts
```

### Instructions

| Instruction | When it runs | What it does |
|---|---|---|
| `FROM` | Build time | Sets the base image |
| `WORKDIR` | Build time | Sets the working directory, creates it if missing |
| `COPY` | Build time | Copies files from local machine into the image |
| `RUN` | Build time | Executes a command and saves result as a new layer |
| `CMD` | Runtime (docker run) | Default command to run when container starts |

## Building

```bash
docker build -t hello-docker .         # build with name hello-docker
docker build -t hello-docker:v2 .      # build with name and tag
```

- `-t` → tag (name) of the image
- `.` → build context (current directory, where Dockerfile is)

## CMD Override

`CMD` is the default command. You can override it by passing a command at the end of `docker run`:

```bash
docker run hello-docker          # runs CMD → Hello, docker!
docker run hello-docker ls       # overrides CMD → lists files
```

## docker commit (not recommended)

You can also create an image from a running container's current state:

```bash
docker commit <container_name> <new_image_name>
```

This is discouraged — changes are not tracked. Always prefer Dockerfile.

## docker cp

Copy files between local machine and a running container:

```bash
docker cp ./file.txt container_name:/usr/src/app/
```

## docker diff

Shows what changed inside a container compared to its original image:

```bash
docker diff container_name
```

- `A` → Added
- `D` → Deleted
- `C` → Changed
