Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A container can run a process as `root` inside the container.

Important:
- Container root ≠ always host root.
- Containers use Linux isolation (namespaces), so root is usually limited to the container.
- However, if there is a container escape vulnerability or excessive permissions, it can become dangerous.

Example:
```
docker run --user root app
```

runs as root inside the container.