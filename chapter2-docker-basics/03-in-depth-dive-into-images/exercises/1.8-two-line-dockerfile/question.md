# Exercise 1.8 - Two Line Dockerfile

By default `devopsdockeruh/simple-web-service:alpine` doesn't have a CMD. Instead, it uses ENTRYPOINT to declare which application is run.

The last argument in `docker run` can be used to give a command or an argument.

Create a Dockerfile and use FROM and CMD to create a brand new image that automatically runs the server.

Tag the new image as "web-server".

As an answer:
- i) Give the Dockerfile you created
- ii) The commands you used to build and run the container
