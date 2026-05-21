# Processes

## What is a Process?

A process is a running program. Your computer runs hundreds of processes at the same time — your browser, VS Code, background update services, etc. Each one is a separate process.

A container works the same way. Multiple processes can run inside a container at the same time.

## PID (Process ID)

Every process gets a unique number called a PID. The first process that starts when the container starts is always **PID 1**. If PID 1 stops, the entire container stops.

## Listing Processes with ps aux

```bash
docker exec -it looper bash
ps aux
```

Example output:

```
USER   PID  COMMAND
root     1   sh -c while true; do date; sleep 1; done   ← main loop (we started this)
root   743   bash                                        ← our exec session
root   795   sleep 1                                     ← the loop waiting 1 second
root   796   ps aux                                      ← the command we just ran
```

- **PID 1** → the looper script, started when the container was created
- **PID 743** → bash shell, started by our `docker exec -it looper bash`
- **PID 795** → the `sleep 1` part of the loop running at that moment
- **PID 796** → `ps aux` itself — a process listing itself
