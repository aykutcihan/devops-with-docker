# Scaling

Docker Compose can run multiple instances of the same service:

```bash
docker compose up --scale whoami=3
```

## Port Clash Problem

If the service has a fixed host port, multiple instances will clash:

```yaml
ports:
  - "8000:8000"  # only one container can bind host port 8000
```

## Solution: Let Docker Pick the Host Port

```yaml
ports:
  - 8000  # container port only — Docker assigns a random host port
```

Then check assigned ports:

```bash
docker compose port --index 1 whoami 8000   # 0.0.0.0:32770
docker compose port --index 2 whoami 8000   # 0.0.0.0:32769
docker compose port --index 3 whoami 8000   # 0.0.0.0:32768
```

## Load Balancer with nginx-proxy

In production, a load balancer sits in front of scaled services. Locally, `jwilder/nginx-proxy` handles this:

```yaml
services:
  whoami:
    image: jwilder/whoami
    environment:
      - VIRTUAL_HOST=whoami.colasloth.com

  proxy:
    image: jwilder/nginx-proxy
    volumes:
      - /var/run/docker.sock:/tmp/docker.sock:ro
    ports:
      - 80:80
```

`nginx-proxy` reads `VIRTUAL_HOST` from each container and routes requests automatically. `colasloth.com` subdomains all resolve to `127.0.0.1` — a DNS trick for local testing.
