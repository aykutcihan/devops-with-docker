# Node.js Development Environment Example

A fully containerized Node.js dev setup with hot-reloading (nodemon).

## Dockerfile

```dockerfile
FROM node:16

WORKDIR /usr/src/app

COPY package* ./

RUN npm install
```

Only copies `package.json` and installs dependencies. Source code is NOT copied — it comes in via a volume mount so changes reflect immediately.

## docker-compose.yml

```yaml
services:
  node-dev-env:
    build: .
    command: npm start
    ports:
      - 3000:3000
    volumes:
      - ./:/usr/src/app
      - node_modules:/usr/src/app/node_modules
    container_name: node-dev-env

volumes:
  node_modules:
```

## How it Works

| Volume | Purpose |
|--------|---------|
| `./:/usr/src/app` | Bind mount — edits on host reflect instantly in container |
| `node_modules:/usr/src/app/node_modules` | Named volume — keeps container's `node_modules` isolated from host |

The second volume is the key trick: without it, the bind mount would overwrite `node_modules` with whatever is (or isn't) on your host. The named volume takes precedence for that specific path, keeping the container-built dependencies intact.

`npm start` typically runs `nodemon` which watches for file changes and restarts the app automatically — so you edit code on the host, and the running container picks it up immediately.
