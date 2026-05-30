# depends_on and restart

## depends_on

Controls startup order between services.

```yaml
services:
  redmine:
    image: redmine:5.1-alpine
    depends_on:
      - db
  db:
    image: postgres:13.2-alpine
```

`db` starts before `redmine` — but `depends_on` only guarantees **start order**, not that the database is ready to accept connections. The app may still crash if it tries to connect before the DB is fully initialized.

## restart

Automatically restarts a container if it stops or crashes.

| Value | Behavior |
|-------|---------|
| `no` | Never restart (default) |
| `always` | Always restart, including after system reboot |
| `unless-stopped` | Restart unless manually stopped — does NOT restart after reboot if manually stopped |
| `on-failure` | Only restart on non-zero exit code |

```yaml
services:
  backend:
    image: backend
    restart: unless-stopped
```

`unless-stopped` is useful when a service depends on another that takes time to start — the container will crash and retry until the dependency is ready.
