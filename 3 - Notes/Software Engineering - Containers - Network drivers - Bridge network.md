Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Creates a private virtual network on a single host.
```
Container A
    |
    |
 Docker bridge
    |
    |
Container B
```
- Containers get private IP addresses.
- Containers on the same bridge can communicate.
- External access uses port mapping.

Example:
```
docker run -p 8080:80 nginx
```

Maps:
```
Host:8080 → Container:80
```

Used for:
- local development
- single-host applications