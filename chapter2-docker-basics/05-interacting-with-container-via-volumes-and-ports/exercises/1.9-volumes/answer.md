# Exercise 1.9 - Volumes

## Commands Used

```powershell
# Create the file first (Docker creates a directory if the file doesn't exist)
[System.IO.File]::WriteAllText("C:/Dev/devops-with-docker/text.log", "")

# Run with bind mount
docker run -v "C:/Dev/devops-with-docker/text.log:/usr/src/app/text.log" devopsdockeruh/simple-web-service
```

## Result

The `text.log` file on the host machine gets populated with timestamps and secret messages from the container in real time.
