Tags: [[__Machine_Learning_Engineering]]

# Introduction
If we use Ray Serve and FastAPI to create a Rest API app, then workflow looks like this:
- Client sends a HTTP request using a specific endpoint to the Ray Serve’s HTTP gateway (a proxy, Starlette ASGI app).
- Ray Serve’s HTTP gateway parses the request and extracts parameters from it.
- Ray Serve’s HTTP gateway sends the parsed request to an actor (a replica process).
- Inside the Actor, FastAPI chooses a correct route handler (a function assigned to the request’s endpoint).
- If the route has dependencies (e.g., DB sessions, auth checks), FastAPI resolves them here.
- Actor executes the code from the route handler.
- FastAPI serializes the result from the route handler (dict -> JSON).
- Actor sends results back to the Ray Serve’s HTTP Gateway.
- Ray Serve’s HTTP Gateway converts result into a HTTP response and send it back to the client.

For example, we can use Ray with FastAPI to create a Rest API endpoint this way:
![[2 - Images/Ray/Screenshot 4.png]]

#MLEngineering 