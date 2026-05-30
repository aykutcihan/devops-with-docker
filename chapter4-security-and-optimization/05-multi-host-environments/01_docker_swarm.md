# Docker Swarm

## Beyond Single-Host Docker

When we have more than one host machine we cannot rely solely on Docker Compose. Docker includes additional tools for automatic deployment, scaling and management of dockerized applications across multiple hosts.

## Docker Swarm Mode

Built into Docker — turns a pool of Docker hosts into a single virtual host.

```bash
docker swarm init
```

Docker Swarm mode is the lightest way of utilizing multiple hosts. Good for small setups (2-3 hosts).

## When to Use Swarm vs Kubernetes

A single tool is rarely optimal for all scenarios:

- **2-3 hosts, hobby project** → Docker Swarm: simpler, less overhead
- **Many hosts, production** → Kubernetes: more powerful, larger ecosystem

## Learning Kubernetes Locally

You can get started with Kubernetes without a cloud account:

| Tool | Description |
|------|-------------|
| k3s | Lightweight Kubernetes distribution |
| k3d | Run k3s inside Docker containers |
| kind | Kubernetes in Docker |

These avoid complicated setup and cloud credit limits.
