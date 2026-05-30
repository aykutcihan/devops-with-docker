# Exercise 2.5 - Answer

## Command

```bash
docker compose up --scale compute=3
```

## Notes

- The project already has a load balancer configured in `docker-compose.yml`
- `--scale compute=3` runs 3 instances of the `compute` service
- The load balancer distributes requests across all instances
- If the button does not turn green, increase the number of instances
