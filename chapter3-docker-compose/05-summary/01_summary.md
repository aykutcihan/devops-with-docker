# Chapter 3 Summary

## What we learned

- Converted multi-container `docker run` setups into a single `docker-compose.yaml`
- Docker Compose automatically creates a shared network — containers reach each other by service name
- Named volumes and bind mounts for data persistence
- `depends_on` and `restart: unless-stopped` for managing startup order
- Nginx as a reverse proxy — single entry point, internal services not exposed
- Port scanning to verify only the right ports are open
- Containerizing development environments for consistent setups across teams

## Final architecture we built

```
Browser → Nginx (:80) → Frontend
                      → Backend → Redis (cache)
                               → PostgreSQL (database)
```

Only Nginx is exposed to the outside. All other services communicate internally via Docker networking.

## Are we production-ready?

Short answer: no. Long answer: depends on the situation. Chapter 4 covers security and optimization to get closer to production-ready setups.
