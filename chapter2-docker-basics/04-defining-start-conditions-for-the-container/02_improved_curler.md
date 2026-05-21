# Improved Curler

## Problem with the old curler

The old curler had an infinite loop — it kept asking "Input website:" every time. You had to attach to the container and type the URL manually. Not suitable for automation.

## Solution with ENTRYPOINT

By using ENTRYPOINT, the URL is passed directly as an argument when running the container:

```bash
docker run curler-v2 helsinki.fi
```

No loop, no manual input. Container starts, runs, and exits.

## How it works

### script.sh
```bash
#!/bin/bash
echo "Searching..";
sleep 1;
curl http://$1;
```

`$1` = the first argument passed to the script. When you run `docker run curler-v2 helsinki.fi`, `helsinki.fi` becomes `$1`.

### Dockerfile
```dockerfile
FROM ubuntu:24.04

RUN apt-get update && apt-get install -y curl

COPY script.sh .

RUN chmod +x script.sh

ENTRYPOINT ["./script.sh"]
```

## Flow

1. `docker run curler-v2 helsinki.fi`
2. Docker creates a container from `curler-v2` image
3. Looks at ENTRYPOINT → `./script.sh`
4. Passes `helsinki.fi` as argument to the script (`$1`)
5. Script runs `curl http://helsinki.fi`
6. Container exits

## Real world use case

In a CI/CD pipeline, you can test a URL after every build:

```bash
docker run curler-v2 myapp.com/health
```

No human interaction needed — fully automated.
