# Exercise 1.3 - Secret Message

## Commands Used

```bash
# Start the container in detached mode
docker run -d devopsdockeruh/simple-web-service:ubuntu

# Enter the running container with a new bash process
docker exec -it fafd80c41953 bash

# Follow the log file inside the container
tail -f ./text.log
```

## Secret Message

`You can find the source code here: https://github.com/docker-hy`
