# Exercise 1.4 - Missing Dependencies

## i) Command to start the process

```bash
docker run -d -it --name missing-dep ubuntu sh -c "while true; do echo 'Input website:'; read website; echo 'Searching..'; sleep 1; curl http://`$website; done"
```

## ii) Commands to fix the problem

```bash
# Enter the running container
docker exec -it missing-dep bash

# Install curl inside the container
apt-get update && apt-get install -y curl

# Exit bash
exit

# Attach to the container and test
docker attach missing-dep
```

## Result

```
Input website:
helsinki.fi
Searching..
<html>
<head><title>301 Moved Permanently</title></head>
<body>
<center><h1>301 Moved Permanently</h1></center>
<hr><center>nginx/1.24.0</center>
</body>
</html>
```
