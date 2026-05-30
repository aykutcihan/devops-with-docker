# Exercise 3.2 - Cloud Pipeline

## Answer

Deployed application: https://express-app-q3mq.onrender.com

## GitHub Actions Workflow (with Render.com deployment)

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

      - name: Deploy to Render
        run: curl "${{ secrets.RENDER_DEPLOY_HOOK }}"
```

The pipeline builds the image, pushes to Docker Hub, then triggers Render.com to pull and deploy the new image via a deploy hook.
