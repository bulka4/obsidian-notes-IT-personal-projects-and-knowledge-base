Tags: [[__Backend_Engineering]]
#BackendEngineering 

# API endpoint
An API endpoint is an API operation (operation we perform using API). For example, for HTTP, it is defined by a method and a path used in a URL, like: `GET /users`.
# API route / Routing
- **API route** - is a definition that maps an API endpoint to a handler.
- **Routing** - is a process of mapping an API endpoint to a handler
- **Routing frameworks** - are used to define routes, e.g. FastAPI, Express
# Handler
A handler is a function that handles an API endpoint. It contains the logic for handling that endpoint and may delegate work to other components (other functions).
# Example
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