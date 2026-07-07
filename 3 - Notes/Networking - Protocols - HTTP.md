Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
HTTP is a protocol used for communication:
1. Client sends a request
2. Server processes it
3. Server sends a response (can sent multiple responses using SSE ([[Backend Engineering - Streaming API Architecture - Server-Sent Events (SSE)|link]]))
# Methods
Common methods available in HTTP:
- **GET** → retrieve data
- **POST** → create data
- **PUT** → replace data
- **PATCH** → partially update data
- **DELETE** → remove data
# Status codes
HTTP responses include a status code:

**Success (2xx)**
- 200 → OK
- 201 → Created
- 204 → No content

**Client errors (4xx)**
- 400 → Bad request
- 401 → Unauthorized
- 403 → Forbidden
- 404 → Not found

**Server errors (5xx)**
- 500 → Internal server error
- 503 → Service unavailable
# Request structure
A HTTP request consists of:
- Headers
- Body
## Headers
Headers are attached to requests and carry extra information:
```
Authorization: Bearer token123Content-Type: application/jsonCache-Control: no-cache
```

They are used for:
- authentication
- caching
- content type
- tracing
- compression
## Body
Body is a JSON that carries data in a request.
# Stateless nature of HTTP
HTTP is **stateless by default**, meaning that each request is independent.

The server does not automatically remember previous requests.

That’s why things like:
- cookies
- sessions
- JWT tokens

exist—to add “memory” on top of HTTP.
# Protocols used
Protocols that different versions of HTTP use:
- Versions 1.1 and 2 uses the TCP protocol
- Version 3 uses QUIC (UDP-based)
# HTTP versions (important evolution)

## HTTP/1.1
- oldest widely used version
- text-based
- one request per connection (limited parallelism)
## HTTP/2
- binary protocol (faster parsing)
- multiplexing (multiple requests at once)
- header compression
## HTTP/3
- built on QUIC (UDP-based)
- faster connection setup
- better performance on unstable networks (mobile)
