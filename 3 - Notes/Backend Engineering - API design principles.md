Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Bulk endpoints
Use bulk endpoints ([[Backend Engineering - Bulk endpoints|link]]) as a request batching ([[Backend Engineering - Request batching|link]]) technique to improve throughput.
# GraphQL
GraphQL is sometimes useful to grab all the data needed by making a single request - [[Backend Engineering - API architectures - GraphQL|link]].
# Consistent naming
Consistency reduces cognitive load.

Common rules:
- Use plural nouns: /users, /orders
- Use lowercase with hyphens or `snake_case` (e.g. `/getUser` or `/get_user`, choose one and stick to it)
# Proper use of HTTP methods
Each method has a semantic meaning:
- **GET** → read data (safe, idempotent)
- **POST** → create or trigger action
- **PUT** → full update (idempotent)
- **PATCH** → partial update
- **DELETE** → remove resource

Bad design:
```
POST /users/updateName
```

Better:
```
PATCH /users/{id}
```
# Design around resources, not actions 
A common principle from Representational State Transfer (REST) is to model APIs around resources (nouns) instead of actions (verbs).

Instead of:
```
/createUser
/getUserData
/deleteUserAccount
```

Prefer:
```
POST   /users
GET    /users/{id}
DELETE /users/{id}
```

This makes the code more readable, easier to understand and work with.
# Statelessness
Each request should contain all the information needed to process it, so we don't need to use additional information from previous requests stored in a state ([[Backend Engineering - Stateful vs stateless service|link]]).

For example, when using the `GET /orders` endpoint:
- In a stateful design - server will return orders for the currently logged in user (so it uses the state which contains an information about currently logged in user). 
- In the statelessness design - server will return orders for the user specified in the request

Stateless design is beneficial as described here - [[Backend Engineering - Stateful vs stateless service|link]].

This is a core constraint of REST-based systems.
# Versioning strategy
APIs evolve. Versioning prevents breaking clients.

Common approaches:
- URL versioning:
    ```
    /v1/users
    /v2/users
    ```
- Header versioning:
    ```
    Accept: application/vnd.myapi.v2+json
    ```

URL versioning is simpler and more common in practice.
# Proper status codes and error handling
Use HTTP status codes correctly:
- 200 OK → success
- 201 Created → resource created
- 204 No Content → success, no body
- 400 Bad Request → validation error
- 401 Unauthorized → not authenticated
- 403 Forbidden → not allowed
- 404 Not Found → resource missing
- 500 Internal Server Error → server issue

Good error response structure:
```json
{
  "error": {
    "code": "USER_NOT_FOUND",
    "message": "User with id 123 does not exist",
    "traceId": "abc-xyz-123"
  }
}
```
# Pagination, filtering, and sorting
Never return unbounded lists, set up some limit on how much data is returned as a response to a request.

Example:
```
GET /users?page=2&limit=50&sort=createdAt&order=desc
```

Optional filtering:
```
GET /users?role=admin&active=true
```
# Idempotency for safety
Idempotency ([[Backend Engineering - Event-driven architecture - Idempotency|link]]) ensures repeated requests don’t cause unintended effects.

Example:
- `PUT /users/123` is idempotent
- `POST /payments` is not (unless you add an idempotency key)

Common pattern:
```
Idempotency-Key: unique-request-id
```

This is critical in payment systems and distributed systems.
# API documentation-first design
Use tools like OpenAPI Specification to define APIs formally.

Benefits:
- Shared contract between backend and frontend
- Auto-generated docs and clients
- Easier testing and validation