# Exercise 3.1 - Your Pipeline

Create a CI/CD pipeline for a simple Node.js/Express app using GitHub Actions and Watchtower.

## Requirements

- Fork or copy the provided Node.js app to your own GitHub repository
- Set up GitHub Actions to build and push a Docker image to Docker Hub on every push to `main`
- Run Watchtower locally to automatically pull and restart the container when a new image is pushed
- Verify the full pipeline: change code → push to GitHub → wait for build and polling → see update in browser

## Watchtower docker-compose.yaml

```yaml
services:
  watchtower:
    image: containrrr/watchtower
    environment:
      - WATCHTOWER_POLL_INTERVAL=60
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```

## GitHub Actions workflow template

```yaml
name: Release

on:
  push:
    branches:
      - main

jobs:
  publish-docker-hub:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4

    - name: Login to Docker Hub
      uses: docker/login-action@v3
      with:
        username: ${{ secrets.DOCKERHUB_USERNAME }}
        password: ${{ secrets.DOCKERHUB_TOKEN }}

    - name: Build and push
      uses: docker/build-push-action@v6
      with:
        push: true
        tags: username/imagename:latest
```

Submit a link to the repository.
