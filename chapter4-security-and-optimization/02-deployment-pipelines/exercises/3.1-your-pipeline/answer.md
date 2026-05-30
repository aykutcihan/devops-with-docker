# Exercise 3.1 - Your Pipeline

## Answer

GitHub repository: https://github.com/aykutcihan/express-app

Docker Hub image: https://hub.docker.com/r/aykutcihan/express-app

## GitHub Actions Workflow

```yaml
name: Release Node.js app

on:
  push:
    branches:
      - main

jobs:
  build:
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
          tags: aykutcihan/express-app:latest
```

Every push to `main` triggers the workflow. It builds the Docker image and pushes it to Docker Hub automatically.
