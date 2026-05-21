# Exercise 1.1 - Getting Started

## Commands Used

```bash
# Start 3 nginx containers in detached mode
docker run -d nginx
docker run -d nginx
docker run -d nginx

# Stop 2 of them
docker container stop interesting_bartik cool_tu
```

## Output of docker ps -a

```
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS                      PORTS     NAMES
053f13246cd4   nginx     "/docker-entrypoint.…"   2 minutes ago   Exited (0) 38 seconds ago             interesting_bartik
ae7b7915dd84   nginx     "/docker-entrypoint.…"   2 minutes ago   Exited (0) 38 seconds ago             cool_tu
da19f0ca69b2   nginx     "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes                80/tcp    hopeful_panini
```
