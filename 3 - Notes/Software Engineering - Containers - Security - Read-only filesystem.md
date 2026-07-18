Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
We can make the container filesystem immutable:
```
docker run --read-only app
```

The application cannot modify files inside the container.

Useful for:
- preventing malware from writing files
- making containers more predictable

Writable data should go to:
- volumes
- databases
- object storage