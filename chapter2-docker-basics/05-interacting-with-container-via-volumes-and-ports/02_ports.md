# Ports

## How it works

A program inside a container listens on a port. By default, that port is not accessible from outside the container. To reach it, you must map a host port to the container port.

## Syntax

```bash
docker run -p host_port:container_port image
```

- **host_port** → the port on your machine
- **container_port** → the port the app listens to inside the container

## Example

```bash
docker run -p 8080:8080 web-server
```

Now opening `http://localhost:8080` in your browser sends the request to the container's port 8080.

## Two steps to open a connection

1. **EXPOSE** in Dockerfile → tells Docker which port the container listens on (informational)
2. **-p flag** in docker run → actually maps the host port to the container port

```dockerfile
EXPOSE 8080
```

```bash
docker run -p 8080:8080 image
```

## Auto port assignment

If you omit the host port, Docker picks a free one automatically:

```bash
docker run -p 8080 image
```

## Security note

`-p 8080:8080` is the same as `-p 0.0.0.0:8080:8080` — open to everyone.

To allow only local access:
```bash
docker run -p 127.0.0.1:8080:8080 image
```
