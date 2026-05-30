# Exercise 3.8 - Multi-Stage Frontend

## Dockerfile

```dockerfile
FROM node:16-alpine AS build-stage
WORKDIR /usr/src/app
COPY . .
RUN npm install && npm run build

FROM nginx:alpine
COPY --from=build-stage /usr/src/app/build /usr/share/nginx/html
EXPOSE 80
```

## Result

| Tag | Size |
|-----|------|
| 3.7 (alpine base) | 949 MB |
| 3.8 (multi-stage + nginx) | 94.3 MB |

Stage 1 builds the React app with node:16-alpine. Stage 2 copies only the compiled static files from `build/` into nginx:alpine — no source code, no node_modules, no build tools in the final image.
