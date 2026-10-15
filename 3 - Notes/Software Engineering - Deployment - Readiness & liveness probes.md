Tags: [[__Software_Engineering]]
#SoftwareEngineering  

# Introduction
- Liveness probe checks whether a service is running
- Readiness probe checks whether a service works correctly, can be used by clients

For example, for a HTTP server:
- Liveness probe checks whether the server is running at all
- Readiness probe checks whether the server can correctly handle requests
# How to implement it
Those checks are implemented by performing some operation and checking its result.

For example, to check a HTTP server, try to make a request to it using an endpoint specifically designed for it, e.g. `GET /health/live`. 

A readiness check might do:
```python
def readiness():
    if not model_loaded():
        return 503

    if not database_connection_works():
        return 503

    return 200
```

The check itself can be an HTTP request, TCP connection, command, function call, database query, etc.