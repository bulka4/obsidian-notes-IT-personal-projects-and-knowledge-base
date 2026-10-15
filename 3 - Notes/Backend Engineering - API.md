Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
An API (Application Programming Interface) is code which one software component uses to interact with another software component.

An API defines how clients can communicate with an API server, including:
- what operations are available
- how requests should be structured
- what responses are returned

APIs can use different communication protocols, such as HTTP, gRPC, or WebSocket.
# Running an API
To run an API, we generally need an API server that:
- receives API requests
- routes them to the appropriate handlers (passes arguments from the request to a proper function) ([[Backend Engineering - API endpoint, route and handler|link]])
- executes the application logic
- and returns responses.

An API server typically consists of:
- a **server** ([[Backend Engineering - API (HTTP, gRPC, etc.) server|link]]) — communicates with clients using the API's protocol, receives requests and sends responses back to clients
- **routing and handlers** ([[Backend Engineering - API endpoint, route and handler|link]]):
	- routing defines how incoming requests are mapped to handlers
	- handlers are functions that contain the logic for handling requests

More information about it can be found here - [[Backend Engineering - Running an API]].
# API server
An API server is a process that:
- accepts API requests
- routes them to handlers ([[Backend Engineering - API endpoint, route and handler|link]])
- and returns responses
# API endpoint
An API endpoint is an API operation (operation we perform using API). For example, for HTTP, it is defined by a method and a path used in a URL, like: `GET /users`.
# API route
An API route is a definition that maps an API endpoint to a handler.
# Handler
A handler is a function that handles an API endpoint. It contains the logic for handling that endpoint and may delegate work to other components (other functions).
# Related topics
1. [[Backend Engineering - Running an API]]
2. [[Backend Engineering - API endpoint, route and handler]]
3. [[Backend Engineering - API (HTTP, gRPC, etc.) server]]