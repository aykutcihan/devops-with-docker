# Why Non-Root Matters

By default, processes inside Docker containers run as **root**. This is a security risk:

- If the container is compromised, the attacker has root-level access inside the container
- With certain misconfigurations (e.g., bind mounts), root inside the container can map to root on the host
- The principle of least privilege: give processes only the permissions they need

## Verifying the User

```bash
docker run myimage whoami
# appuser
```
