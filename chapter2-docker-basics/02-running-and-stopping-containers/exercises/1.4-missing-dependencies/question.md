# Exercise 1.4 - Missing Dependencies

Start a Ubuntu image. Then, with the process running, run the following script:

```bash
sh -c "while true; do echo 'Input website:'; read website; echo 'Searching..'; sleep 1; curl http://`$website; done"
```

The small script uses the command line tool `curl` to load a URL and print it to screen. If you try the script, it does not work:

```
Input website:
helsinki.fi
Searching..
sh: 1: curl: not found
```

Your task is to fix the error by installing `curl` inside the container.

As an answer:
- i) Write the command you used to start the process.
- ii) Write the command(s) you used to fix the ensuing problems.
