Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
An API server is a process that:
- accepts API requests
- routes them to handlers ([[Backend Engineering - API endpoint, route and handler|link]]), i.e. chooses a proper handler to handle the request (using routing defined by a routing framework) and executes it
- and returns responses

There are different API servers for different protocols, for example:
- HTTP server - for HTTP requests
- gRPC server - for gRPC requests
- WebSocket server - for WebSocket messages
- TCP server - for TCP data

Example API servers:
- Node.js
- Uvicorn