# Exercise 1.5 - Sizes of Images

In Exercise 1.3 we used `devopsdockeruh/simple-web-service:ubuntu`.

Here is the same application but instead of Ubuntu it is using Alpine Linux: `devopsdockeruh/simple-web-service:alpine`.

Pull both images and compare the image sizes.

Go inside the Alpine container and make sure the secret message functionality is the same. Alpine version doesn't have bash but it has sh, a more bare-bones shell.

- What is the size of the alpine image (in MB)?
- What is the size of the ubuntu image (in MB)?
