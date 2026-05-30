# Exercise 3.4 - Building Images from Inside a Container

Containerize the script from Exercise 3.3. Use `docker.sock` mounting so Docker commands work inside the container. Pass Docker Hub credentials as environment variables.

## Usage

```bash
docker run -e DOCKER_USER=username \
  -e DOCKER_PWD=password \
  -v /var/run/docker.sock:/var/run/docker.sock \
  builder github_repo dockerhub_repo
```

## Requirements

- Create a Dockerfile for the builder image
- Use `ENTRYPOINT` in the Dockerfile to run the script
- Read `DOCKER_USER` and `DOCKER_PWD` from environment variables (not hardcoded)
- Mount `/var/run/docker.sock` to enable Docker commands inside the container

Submit the Dockerfile and the script.
