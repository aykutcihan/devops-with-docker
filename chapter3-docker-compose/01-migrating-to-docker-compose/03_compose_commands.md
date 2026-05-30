# Docker Compose Commands

| Command | What it does |
|---------|-------------|
| `docker compose up` | Start all services (foreground) |
| `docker compose up -d` | Start all services (detached/background) |
| `docker compose down` | Stop and remove containers |
| `docker compose down -v` | Also remove named volumes |
| `docker compose logs` | View logs from all services |
| `docker compose logs -f` | Follow logs in real time |
| `docker compose ps` | List running compose services |

## up vs down

- `up` creates and starts containers
- `down` stops and removes them — volumes persist unless `-v` is added
