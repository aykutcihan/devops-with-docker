# Exercise 1.16 - Cloud Deployment

## Dockerfile

```dockerfile
FROM devopsdockeruh/simple-web-service:alpine
CMD ["server"]
```

## What was done

Built the web-server image from Exercise 1.8, pushed it to Docker Hub as `aykutcihan/web-server`, then deployed to Render.com using the existing image option.

## Running App

https://web-server-ssst.onrender.com
