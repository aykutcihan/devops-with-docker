# Image and Container

## Relationship
Containers are instances of images. The most common mistake is to confuse the two.

- Dockerfile → the recipe for building an image
- Image → the recipe and ingredients for creating a container
- Container → the ready-to-eat meal, the running instance

We are 2 recipes deep: Dockerfile is written by us, image is built by the machine from that Dockerfile, and containers are created from the image.

## Image
A Docker image is an immutable file — it can never be changed after it is created. A new image is created by starting from a base image and adding new layers on top of it.

Images are built from a file called **Dockerfile**:

```dockerfile
FROM <image>:<tag>

RUN <install some dependencies>

CMD <command that is executed on docker container run>
```

- `FROM` → base image to start from
- `RUN` → commands to run during build (e.g. install dependencies)
- `CMD` → command to run when the container starts

List all images:
```bash
docker image ls
```

## Container
A container is a running instance of an image. Containers are isolated environments on the host machine. They can interact with each other and the host via defined methods (TCP/UDP).

List running containers:
```bash
docker container ls
# or shorthand:
docker ps
```

List all containers including stopped ones:
```bash
docker container ls -a
# or shorthand:
docker ps -a
```

## Container Status
- `Up` → container is running
- `Exited (0)` → container finished successfully and stopped

## Key Points
- One image can produce many containers
- Deleting a container does not affect the image
- If you run `hello-world` twice: 1 image downloaded, 2 containers created
