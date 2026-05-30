# CI/CD Basics

CI/CD automates the process of moving code from a commit into production — without manual intervention.

## The Problem

Every time you push code:
1. Someone has to build the Docker image
2. Push it to Docker Hub
3. Pull it on the server
4. Restart the container

This is repetitive, error-prone, and slow. CI/CD automates all of it.

## The Pipeline

Two tools work together:

| Tool | Role |
|------|------|
| **GitHub Actions** | Builds the Docker image and pushes it to Docker Hub on every `git push` |
| **Watchtower** | Runs on the server, polls Docker Hub, and automatically pulls + restarts the container when a new image appears |

Flow:
```
git push → GitHub Actions → build image → push to Docker Hub → Watchtower detects → pulls image → restarts container
```
