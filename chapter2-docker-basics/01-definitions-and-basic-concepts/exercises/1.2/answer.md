# Exercise 1.2 - Cleanup

## Commands Used

```bash
# Remove all 3 nginx containers (including the running one with --force)
docker container rm interesting_bartik cool_tu hopeful_panini --force

# Remove the nginx image
docker image rm nginx
```

## Output of docker ps -a (after cleanup)
No nginx containers remain. Only pre-existing project containers are listed.

## Output of docker image ls (after cleanup)
No nginx image remains. Only pre-existing project images are listed.
