# Exercise 2.3 - Answer

## docker-compose.yaml

```yaml
services:
  frontend:
    image: frontend
    ports:
      - "5001:5001"

  backend:
    image: backend
    ports:
      - "8080:8080"
    environment:
      - REQUEST_ORIGIN=http://localhost:5001
```

## Notes

- `REACT_APP_BACKEND_URL=http://localhost:8080` is already baked into the frontend image at build time — cannot be overridden at runtime
- `REQUEST_ORIGIN` tells the backend to allow CORS requests from the frontend
