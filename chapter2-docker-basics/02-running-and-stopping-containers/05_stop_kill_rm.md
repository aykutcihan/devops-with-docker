# stop vs kill vs rm

## docker stop

Sends a polite stop signal (SIGTERM) to the container. Waits for the processes to finish cleanly before shutting down.

```bash
docker stop looper
```

Use when you want the container to shut down gracefully.

## docker kill

Forces the container to stop immediately. Does not wait. Sends SIGKILL directly.

```bash
docker kill looper
```

Use when `stop` does not work — for example when the process ignores the stop signal (like our looper).

## docker rm

Removes the container completely. The container must be stopped first. After `rm`, the container is gone from `docker ps -a`.

```bash
docker rm looper
```

## Combining kill and rm

```bash
docker kill looper
docker rm looper

# or with --force flag (same result):
docker rm --force looper
```

## Summary

| Command | What it does |
|---|---|
| `stop` | Politely asks the container to stop, waits for it |
| `kill` | Forces the container to stop immediately |
| `rm` | Deletes the stopped container completely |

## --rm flag on docker run

Adding `--rm` to `docker run` automatically removes the container when it exits — no need to run `docker rm` manually.

```bash
docker run -d --rm -it --name looper-it ubuntu sh -c "while true; do date; sleep 1; done"
```
