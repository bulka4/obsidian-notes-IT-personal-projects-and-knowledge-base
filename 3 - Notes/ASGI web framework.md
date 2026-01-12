Tags: [[__Web_Development]]
#WebDevelopment 

# Introduction
ASGI web framework allows us to program an app that can communicate with other apps. Other apps will be able to make requests to our ASGI app, and it will send back a response. That communication can be done using different protocols, for example Rest API.

ASGI web framework handles:
- Routing
	- Which endpoints ([[Endpoint|link]]) executes which functions
- Validates and serializes a request and a response
	- For example checks if required fields exist and data types
	- Serialization means converting request data into objects in a programming language we use (like dictionary in Python) and objects into response
- Defines functions assigned to endpoints
- Middleware (authentication, logging etc.)

For example, FastAPI is an ASGI web framework and using it, we can write such code to create an endpoint for our app:
```python
class UserOut(BaseModel):
    id: int
    email: str

# Define endpoint
@app.post("/users", response_model=UserOut)
def create_user(user: UserIn):
    return user
```
# ASGI callable
Using an ASGI framework, we create a bunch of functions used to handle different types of request for different endpoints.

ASGI framework then, creates a single callable (a function that can be called), called ASGI callable, which dispatches incoming requests to the proper endpoint function.

It might look for example like that (a simplified version):
```python
def app(request):
    if request.path == "/users" and request.method == "GET":
        return list_users()
    if request.path == "/users" and request.method == "POST":
        return create_user()
```