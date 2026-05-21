# Exercise 1.2 - Cleanup

Stop all your containers.

Now you have containers and some images that are no longer in use and are taking up space. Running `docker ps -a` and `docker image ls` will confirm this.

Clean the Docker daemon by removing all images and containers. If you have some other existing projects running and they should not be removed, you might want to use `grep` (or similar) for the filtering in the listing commands.

As an answer:
- i) Give the commands you used to remove the images and containers.
- ii) Give the output for `docker ps -a` and `docker image ls` after clean up.
