# Chapter 4 Summary - Security and Optimization

In this chapter, we explored several crucial aspects essential for running containers in production environments. We delved into the importance of CI/CD pipelines in ensuring a seamless deployment process and highlighted the significance of running containers as non-root users for enhanced security. Additionally, we examined strategies for minimizing container size and discussed the advantages of maintaining a minimal footprint.

> A logical next step is the course **DevOps with Kubernetes**.

## What We Covered

### 1. Official Images and Trust

- Docker Hub distinguishes between official, verified publisher, and community images
- Official images are maintained by Docker and the upstream project teams
- Always prefer official or verified publisher images in production
- Check image provenance: `docker image inspect` shows build metadata

### 2. Deployment Pipelines

- CI/CD automates: test → build → push → deploy
- GitHub Actions triggers on push, builds Docker image, pushes to Docker Hub
- Watchtower polls Docker Hub and auto-restarts containers with updated images
- Render.com deploy hooks allow triggering deployments from CI pipelines
- `docker.sock` mounting enables Docker commands inside containers (Docker-in-Docker pattern)

### 3. Non-Root Users

- Default container processes run as root — a security risk
- Use `USER` instruction to switch to a non-root user
- Create the user before switching: `RUN useradd -r appuser`
- Use `COPY --chown` to set file ownership at copy time
- Apps must use ports >= 1024 when running as non-root

### 4. Optimizing Image Size

- **Multi-stage builds**: build in one stage, copy artifacts to minimal final stage
- **Alpine base**: ~7MB vs ~77MB for Ubuntu
- **Layer ordering**: copy dependencies before source code for better cache hits
- **Combine RUN commands**: fewer layers, smaller total size
- **Clean up in the same layer**: `apt-get clean` in a separate RUN has no effect on size
- **.dockerignore**: exclude unnecessary files from build context

### 5. Multi-Host Environments

- Docker Swarm: built-in, simple multi-host orchestration
- Kubernetes: industry standard, complex but powerful
- Managed services (GKE, EKS, AKS) handle infrastructure complexity
- Most production workloads today run on Kubernetes

## Key Commands

```bash
# Security
docker run --user 1000:1000 myimage    # Run as specific UID:GID
docker inspect myimage | grep User     # Check image default user

# Optimization
docker images                          # Check image sizes
docker history myimage                 # Inspect layers
docker build --no-cache .              # Force fresh build

# Multi-host
docker swarm init                      # Initialize swarm
docker stack deploy -c compose.yml app # Deploy to swarm
docker service scale app_web=5         # Scale a service
```

## Security Checklist

- [ ] Use non-root user in Dockerfile
- [ ] Use official or verified base images
- [ ] Scan images for vulnerabilities (`docker scout`)
- [ ] Never hardcode secrets — use environment variables or secrets managers
- [ ] Keep base images updated
- [ ] Use read-only filesystems where possible (`--read-only`)
- [ ] Limit container capabilities (`--cap-drop ALL`)

## Course Completion

This chapter completes the core Docker curriculum:

| Chapter | Topic |
|---------|-------|
| Chapter 1 | Definitions and Basic Concepts |
| Chapter 2 | Docker Compose |
| Chapter 3 | Volumes, Networking, Development |
| Chapter 4 | Security and Optimization |
