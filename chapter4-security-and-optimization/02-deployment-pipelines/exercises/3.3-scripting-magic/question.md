# Exercise 3.3 - Scripting Magic

Write a script that clones a GitHub repository, builds its Docker image, and pushes it to Docker Hub.

## Requirements

The script takes two arguments:
1. GitHub repository (e.g. `mluukkai/express_app`)
2. Docker Hub repository (e.g. `mluukkai/testing`)

## Usage

```bash
./builder.sh mluukkai/express_app mluukkai/testing
```

## What the script should do

1. Clone `https://github.com/<github_repo>`
2. Build the Docker image from the cloned repo's Dockerfile
3. Tag and push it to `<dockerhub_repo>:latest`

Submit the script.
