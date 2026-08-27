Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
An API endpoint is an API operation (operation we perform using API). For example, for HTTP, it is defined by a method and a path used in a URL, like: `GET /users`.

An API route is a definition that maps an API endpoint to a handler.

A handler is a function that handles an API endpoint. It contains the logic for handling that endpoint and may delegate work to other components (other functions).

For example, in a `FastAPI` code like this:
```python
@app.get("/users")
def get_users():
    users = database.get_users()
    return users
```
- `GET /users` - This operation is the endpoint
- `@app.get("/users")` - this decorator is the route definition
- `get_users()` - this function is the handler