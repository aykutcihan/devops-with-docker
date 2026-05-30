# Multi-Host Environments

## Beyond Single-Host Docker

So far everything has run on a single machine. Production systems typically span multiple hosts for:

- **High availability**: if one host fails, others continue serving
- **Scalability**: distribute load across many machines
- **Geographic distribution**: run containers close to users

## Docker Swarm

Docker's built-in orchestration for multi-host deployments.

### Initializing a Swarm

```bash
# On the manager node
docker swarm init --advertise-addr <manager-ip>

# Output includes a join token for workers
docker swarm join --token <token> <manager-ip>:2377
```

### Deploying a Stack

Docker Swarm uses the same `docker-compose.yml` format with `deploy` keys:

```yaml
version: "3.8"
services:
  web:
    image: nginx:alpine
    deploy:
      replicas: 3
      restart_policy:
        condition: on-failure
    ports:
      - "80:80"
```

```bash
docker stack deploy -c docker-compose.yml myapp
docker stack services myapp
docker stack ps myapp
```

### Swarm Concepts

| Concept | Description |
|---------|-------------|
| Manager node | Controls the swarm, schedules tasks |
| Worker node | Runs containers, reports to manager |
| Service | Definition of how to run a container |
| Task | A running container instance |
| Replica | Number of instances to run |

## Kubernetes

The industry-standard container orchestration platform.

### Key Differences from Docker Swarm

| Feature | Docker Swarm | Kubernetes |
|---------|-------------|------------|
| Complexity | Simple | Complex |
| Learning curve | Low | High |
| Production use | Less common | Industry standard |
| Auto-scaling | Manual | Built-in HPA |
| Self-healing | Basic | Advanced |
| Ecosystem | Limited | Massive |

### Kubernetes Objects

- **Pod**: Smallest deployable unit (one or more containers)
- **Deployment**: Manages replica sets of pods
- **Service**: Exposes pods via stable network endpoint
- **Ingress**: Manages external HTTP/S access
- **ConfigMap / Secret**: Configuration and sensitive data

### Basic Kubernetes Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-app
          image: myimage:latest
          ports:
            - containerPort: 3000
```

## Managed Kubernetes Services

Running Kubernetes yourself is complex. Cloud providers offer managed versions:

| Provider | Service |
|----------|---------|
| Google Cloud | GKE (Google Kubernetes Engine) |
| AWS | EKS (Elastic Kubernetes Service) |
| Azure | AKS (Azure Kubernetes Service) |
| DigitalOcean | DOKS |

Managed services handle control plane management, upgrades, and scaling infrastructure.

## When to Use What

- **Single host, development**: `docker compose`
- **Small production, simple needs**: Docker Swarm
- **Large production, complex needs**: Kubernetes
- **Learning / hobby projects**: Docker Compose on a single VPS
