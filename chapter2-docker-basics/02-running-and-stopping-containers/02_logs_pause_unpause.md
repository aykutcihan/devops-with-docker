# Logs, Pause and Unpause

## docker logs

Containers run in the background with `-d`. You cannot see their output directly. `docker logs` lets you read what the container has printed.

```bash
docker logs looper          # show all logs so far
docker logs -f looper       # follow logs in real time (like a live feed)
```

Press `Ctrl+C` to stop following. The container keeps running.

## docker pause / unpause

`pause` freezes all processes inside the container. The container does not stop — it stays in memory, but nothing moves forward.

```bash
docker pause looper         # freeze all processes inside the container
docker unpause looper       # resume from where it stopped
```

### What exactly gets paused?

Only the processes inside that container are frozen. The Docker engine keeps running and manages all other containers normally. Only `looper`'s processes are paused.

Think of it like pressing pause on a video. The TV (Docker engine) is still on — only the video (container process) is frozen.
