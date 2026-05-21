# Interactive Flags

## Why Do We Need Flags?

When you run `docker run ubuntu`, the container starts and tries to open a shell — but nothing happens and it immediately exits. The container opened a shell and waited, but no one connected to it, so it shut down.

Think of it like making a phone call with the microphone turned off. The other side says "hello?" — no sound comes through — they hang up.

Flags solve this problem.

## Flags

| Flag | Description |
|---|---|
| `-t` | Opens a terminal (tty) inside the container |
| `-i` | Passes your keyboard input (STDIN) to the container |
| `-it` | Both together — lets you type commands inside the container's shell |
| `-d` | Detached mode — container runs in the background, terminal stays free |
| `--name` | Gives the container a custom name instead of a random one |
| `--rm` | Automatically removes the container after it exits |

## Difference Between -t and -it

- `-t` alone → terminal opens inside the container but your input does not reach it — it freezes
- `-it` together → terminal opens AND your input is sent to the container — you can type commands

## Shell

A shell is the program that reads your commands and executes them. When you open a terminal in VS Code, that terminal is running a shell. Inside an Ubuntu container, the default shell is **bash**.

When you run `docker run -it ubuntu`, you enter the bash shell inside the container. From there you can run Linux commands like `ls`, `cd`, `apt-get install`, etc.

To exit the container shell, type `exit`.
