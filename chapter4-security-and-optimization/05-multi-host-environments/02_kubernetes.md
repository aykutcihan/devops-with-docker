# Kubernetes

The de facto standard for orchestrating containers in large multi-host environments.

## Why Kubernetes

- Highly customizable
- Large community
- Robust features (auto-scaling, self-healing, rolling deployments)

Drawback: higher learning curve compared to Docker Swarm.

## Key Concepts

| Term | Description |
|------|-------------|
| Cluster | The full Kubernetes environment — all nodes together |
| Node | A single host machine (VM or physical) in the cluster |
| Pod | Smallest deployable unit — wraps one or more containers |
| Container | The actual running process inside a Pod |
| Service | Stable network endpoint that exposes Pods |
| Volume | Persistent storage attached to a Pod |
| Ingress | Manages external HTTP/S access into the cluster |
| kubectl | CLI tool to send instructions to the cluster |

## Cluster Architecture

```
Your Computer
    │ kubectl apply
    ▼
Control Plane (Master Node)
    │ schedules Pods
    ▼
Worker Nodes (Host Machines)
    ├── Node 1: Pod (Container A, Container B)
    ├── Node 2: Pod (Container C)
    └── Node 3: Pod (Container D)
```

## Managed Kubernetes Services

Running Kubernetes yourself is complex. Cloud providers offer managed control planes:

| Provider | Service |
|----------|---------|
| Google Cloud | GKE (Google Kubernetes Engine) |
| AWS | EKS (Elastic Kubernetes Service) |
| Azure | AKS (Azure Kubernetes Service) |
| DigitalOcean | DOKS |

Most common production setup: use a managed service, focus on your application not the cluster.
