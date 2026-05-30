# Exercise 3.10 - Optimal Sized Image

Project: **express-app** (simple Node.js/Express application)

## Dockerfile Before

```dockerfile
FROM node:16
COPY . .
RUN npm install
CMD node index.js
```

Size: **1.35 GB**

## Dockerfile After

```dockerfile
FROM node:16-alpine

WORKDIR /usr/src/app

COPY --chown=node:node package*.json ./

RUN npm install --omit=dev

COPY --chown=node:node . .

USER node

EXPOSE 8080

CMD ["node", "index.js"]
```

Size: **183 MB**

## Optimizations Applied

| Optimization | Reason |
|---|---|
| `node:16` → `node:16-alpine` | Alpine base is ~8 MB vs ~900 MB |
| `WORKDIR` | Clean working directory instead of root |
| Separate `package*.json` copy | Better layer caching — npm install only reruns when dependencies change |
| `--omit=dev` | Excludes devDependencies from production image |
| `COPY --chown=node:node` | Sets file ownership without extra RUN layer |
| `USER node` | Non-root user, node image has built-in `node` user |
| CMD as JSON array | Correct signal handling (SIGTERM reaches the process) |
