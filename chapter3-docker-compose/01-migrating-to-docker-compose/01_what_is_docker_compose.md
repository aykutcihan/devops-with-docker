# What is Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications using a single YAML file.

## The Problem it Solves

Running multiple containers manually means:
- Multiple `docker run` commands with long flags
- Remembering all `-p`, `-v`, `-e`, `--network` options
- Starting containers in the right order by hand

Docker Compose replaces all of this with one file and one command.

## How it Works

1. Define all services in `docker-compose.yaml`
2. Run `docker compose up`
3. All containers start together, on the same network, with the right config
