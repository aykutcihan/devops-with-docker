# ENTRYPOINT vs CMD

## CMD

The default command that runs when a container starts. It can be completely overridden by adding a command at the end of `docker run`.

```bash
docker run hello-docker        # runs CMD → Hello, docker!
docker run hello-docker ls     # overrides CMD → lists files instead
```

## ENTRYPOINT

The main program of the container. It cannot be overridden. Whatever you pass at the end of `docker run` becomes an argument to ENTRYPOINT, not a replacement.

```bash
docker run yt-dlp https://youtube.com/...
# runs: yt-dlp https://youtube.com/...
# ENTRYPOINT stays, URL is passed as argument
```

## Both Together

When used together, ENTRYPOINT is the fixed program and CMD provides the default argument. The CMD can be overridden at runtime.

```dockerfile
ENTRYPOINT ["/usr/local/bin/yt-dlp"]
CMD ["https://www.youtube.com/watch?v=Aa55RKWZxxI"]
```

```bash
docker run yt-dlp                          # uses default CMD URL
docker run yt-dlp https://other-video.com  # overrides CMD with new URL
```

In both cases, yt-dlp (ENTRYPOINT) always runs — only the argument (CMD) changes.

## Summary

| | ENTRYPOINT | CMD |
|---|---|---|
| Purpose | Main program | Default argument |
| Can be overridden? | No | Yes |
| What happens when you add args to docker run | Args are passed to ENTRYPOINT | CMD is replaced |

## Best Practice

Use ENTRYPOINT when your image has one specific purpose (like downloading videos). Use CMD to provide sensible defaults that users can easily override.
