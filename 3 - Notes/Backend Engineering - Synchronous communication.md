Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Synchronous (request/response)
One system waits for another to reply.
- HTTP/REST (most common)
- gRPC
- GraphQL (still usually synchronous at transport level)

**Key traits:**
- Simple to reason about
- Tight coupling in real-time
- Risk of cascading failures if one service is slow/down

Example:
- Frontend → Backend API → Database query → response
# Asynchronous communication
[[Backend Engineering - Asynchronous communication]].