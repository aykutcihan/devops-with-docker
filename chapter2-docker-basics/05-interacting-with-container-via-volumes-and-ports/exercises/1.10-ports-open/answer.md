# Exercise 1.10 - Ports Open

## Command Used

```bash
docker run -p 8080:8080 web-server
```

## Result

Opening `http://localhost:8080` in the browser returns:

```json
{"message":"You connected to the following path: /","path":"/"}
```
