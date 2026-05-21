# attach vs exec

## docker attach

Connects you to the already running process (PID 1) inside the container. You see its output directly.

```bash
docker attach looper
```

**Warning:** If you press `Ctrl+C`, you kill the process — and the container stops.

## docker attach --no-stdin

Connects to the running process but does not send your input. `Ctrl+C` only disconnects you — the container keeps running.

```bash
docker attach --no-stdin looper
```

Use this when you want to observe a container's output safely without accidentally stopping it.

## docker exec

Runs a new, separate command inside a running container. The container does not stop, the existing process keeps going.

```bash
docker exec looper ls -la              # run a single command
docker exec -it looper bash            # open an interactive bash shell inside
```

## Key Difference

| | attach | exec |
|---|---|---|
| What it does | Connects to the existing PID 1 process | Starts a brand new process |
| Ctrl+C effect | Stops the container (without --no-stdin) | Only exits the exec session |
| Use case | Observe or interact with the main process | Run extra commands without touching the main process |
