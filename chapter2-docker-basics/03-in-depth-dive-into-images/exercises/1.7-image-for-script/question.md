# Exercise 1.7 - Image for Script

Create a new file `script.sh` with the following contents:

```bash
#!/bin/bash
while true
do
  echo "Input website:"
  read website; echo "Searching.."
  sleep 1; curl http://$website
done
```

Create a Dockerfile for a new image that starts from `ubuntu:24.04` and:
- Installs curl
- Copies the script file into the image
- Sets it to run on container start using CMD

Build the image with the name "curler".

The following should work:

```bash
docker build -t curler .
docker run -it curler
```

Give your Dockerfile as an answer.
