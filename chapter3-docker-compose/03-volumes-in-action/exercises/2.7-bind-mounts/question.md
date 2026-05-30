# Exercise 2.7 - Bind Mounts

Replace the Postgres named volume from Exercise 2.6 with a bind mount at `./database`.

## Instructions

- Use a bind mount instead of a named volume for the database
- The data should persist across `docker compose down` / `docker compose up` cycles
- Verify that data is still there after restarting

Submit the `docker-compose.yaml`.
