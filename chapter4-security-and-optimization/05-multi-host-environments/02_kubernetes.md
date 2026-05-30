# Kubernetes

The industry-standard container orchestration platform.

## Docker Swarm vs Kubernetes

| Feature | Docker Swarm | Kubernetes |
|---------|-------------|------------|
| Complexity | Simple | Complex |
| Learning curve | Low | High |
| Production use | Less common | Industry standard |
| Auto-scaling | Manual | Built-in HPA |
| Self-healing | Basic | Advanced |
| Ecosystem | Limited | Massive |

## Kubernetes Objects

- **Pod**: Smallest deployable unit (one or more containers)
- **Deployment**: Manages replica sets of pods
- **Service**: Exposes pods via stable network endpoint
- **Ingress**: Manages external HTTP/S access
- **ConfigMap / Secret**: Configuration and sensitive data

## Basic Deployment

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

| Scenario | Tool |
|----------|------|
| Development, single host | `docker compose` |
| Small production, simple needs | Docker Swarm |
| Large production, complex needs | Kubernetes |
| Learning / hobby | Docker Compose on a VPS |
