# Exercise 3.4 - Building Images from Inside a Container

## Answer

### Dockerfile

```dockerfile
FROM docker:latest
RUN apk add --no-cache git
WORKDIR /usr/src/app
COPY builder.sh .
RUN chmod +x builder.sh
ENTRYPOINT ["./builder.sh"]
```

### builder.sh

```bash
#!/bin/bash
GITHUB_REPO=$1
DOCKERHUB_REPO=$2

docker login -u $DOCKER_USER -p $DOCKER_PWD
git clone https://github.com/$GITHUB_REPO
REPO_NAME=$(basename $GITHUB_REPO)
cd $REPO_NAME
docker build -t $DOCKERHUB_REPO .
docker push $DOCKERHUB_REPO
```

## Usage

```bash
docker run -e DOCKER_USER=username \
  -e DOCKER_PWD=password \
  -v /var/run/docker.sock:/var/run/docker.sock \
  builder mluukkai/express_app mluukkai/testing
```

The `docker:latest` base image includes the Docker CLI. Git is added via apk. The `docker.sock` mount allows the container to communicate with the host's Docker daemon, enabling Docker commands inside the container.
