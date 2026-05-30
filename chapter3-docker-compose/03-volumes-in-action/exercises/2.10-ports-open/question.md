# Exercise 2.10 - Ports Open

Verify that only port 80 (Nginx) is accessible from outside. Frontend and backend should not be directly reachable.

## Instructions

- Make sure `ports` are only defined for the Nginx service
- Use a port scanner (e.g. Nmap) to verify:

```bash
nmap localhost
```

Expected result: only port 80 is open. Ports 8080 (backend) and 5000/5001 (frontend) should not appear.

Submit the Nmap output.
