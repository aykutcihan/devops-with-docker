# Volumes and Bind Mounts

## Problem

Files created inside a container are lost when the container is removed. They live only in the container's ephemeral storage.

## Solution: Bind Mount

A bind mount connects a file or directory on the host machine to a file or directory inside the container. Whatever the container writes goes directly to the host file — and stays there even after the container is removed.

## Syntax

```bash
docker run -v "host_path:container_path" image
```

## Examples

Mount a directory:
```bash
docker run -v "$(pwd):/mydir" yt-dlp https://youtube.com/...
```

Mount a single file:
```bash
docker run -v "C:/Dev/devops-with-docker/text.log:/usr/src/app/text.log" devopsdockeruh/simple-web-service
```

## Important Note on Windows

If the file does not exist on the host, Docker creates it as a **directory**. Always create the file first:

```powershell
[System.IO.File]::WriteAllText("C:/path/to/file.log", "")
```

## Key Points

- Volume = shared file/directory between host and container
- Changes made inside the container reflect on the host immediately
- Changes made on the host reflect inside the container immediately
- Data persists after the container is stopped or removed
- Volumes can also be shared between multiple containers
