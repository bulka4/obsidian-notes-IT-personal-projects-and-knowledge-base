Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
To run an API, we generally need an API server that receives API requests, routes them to the appropriate handlers, executes the application logic, and returns responses.

An API server typically consists of:
- a **server** ([[Backend Engineering - API (HTTP, gRPC, etc.) server|link]]) — communicates with clients using the API's protocol, receiving requests and sending responses
- **routing and handlers** ([[Backend Engineering - API endpoint, route and handler|link]]):
	- routing defines how incoming requests are mapped to handlers
	- handlers are functions that contain the logic for handling requests
# Example
For example, to run API we can use:
## Uvicorn + FastAPI
- **Uvicorn** — HTTP server that receives HTTP requests and sends HTTP responses
- **FastAPI** — web framework that provides routing and request handling
- **Handler** — function that contains the logic for a particular endpoint

```python
@app.get("/users")
def get_users():
    users = database.get_users()
    return users
```
## Node.js + Express
- **Node.js HTTP server** — receives HTTP requests and sends HTTP responses
- **Express** — provides routing and request handling
- **Handler** — function that contains the logic for a particular endpoint

```JavaScript
app.get("/users", (req, res) => {
    const users = database.getUsers();
    res.json(users);
});
```
