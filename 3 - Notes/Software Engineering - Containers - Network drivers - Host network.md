Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
The container uses the host's network directly.
```
Container
    |
    |
Host network interface
    |
Internet
```

No separate container network namespace.

Example:
```
docker run --network host nginx
```

Advantages:
- very fast
- no network translation

Disadvantages:
- less isolation
- port conflicts possible

Used for:
- high-performance networking
- monitoring tools