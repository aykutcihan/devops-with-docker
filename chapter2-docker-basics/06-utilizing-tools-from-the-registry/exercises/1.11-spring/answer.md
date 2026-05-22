# Exercise 1.11 - Spring

## Dockerfile

```dockerfile
FROM amazoncorretto:8

EXPOSE 8080

WORKDIR /usr/src/app

COPY . .

RUN ./mvnw package

CMD ["java", "-jar", "./target/docker-example-1.1.3.jar"]
```

## Commands

```bash
docker build -t spring-project .
docker run -p 8080:8080 spring-project
```
