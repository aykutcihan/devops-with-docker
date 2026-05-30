# Exercise 3.3 - Scripting Magic

## Answer

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
export DOCKER_USER=myusername
export DOCKER_PWD=mypassword
./builder.sh mluukkai/express_app mluukkai/testing
```

The script takes the GitHub repo and Docker Hub repo as arguments, clones the source, builds the image, and pushes it.
