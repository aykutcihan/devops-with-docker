# Docker Swarm

## Why Multi-Host?

So far everything has run on a single machine. Production systems typically span multiple hosts for:

- **High availability**: if one host fails, others continue serving
- **Scalability**: distribute load across many machines
- **Geographic distribution**: run containers close to users

## Initializing a Swarm

```bash
# On the manager node
docker swarm init --advertise-addr <manager-ip>

# Join workers using the token from the output
docker swarm join --token <token> <manager-ip>:2377
```

## Deploying a Stack

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

## Swarm Concepts

| Concept | Description |
|---------|-------------|
| Manager node | Controls the swarm, schedules tasks |
| Worker node | Runs containers, reports to manager |
| Service | Definition of how to run a container |
| Task | A running container instance |
| Replica | Number of instances to run |
