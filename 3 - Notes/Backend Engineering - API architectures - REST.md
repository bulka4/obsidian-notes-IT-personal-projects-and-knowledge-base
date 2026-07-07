Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
REST (Representational State Transfer) is an architectural style for designing web APIs. It is not a protocol and not a library. It is built on top of HTTP ([[Networking - Protocols - HTTP|link]]).

REST models our application as a collection of resources. A resource is simply an object in our system, for example:
- `/users`
- `/orders`
- `/products`
- `/employees`

Clients interact with these resources using standard HTTP methods, for example:
```
GET    /users        → retrieve users
GET    /users/42     → retrieve user 42
POST   /users        → create a new user
PATCH  /users/42     → update user 42
DELETE /users/42     → delete user 42
```

The URL identifies what we're working with (the resource), while the HTTP method specifies what action to perform.
# Key features
## Resource-oriented
URLs represent **things**, not actions.

Good:
```
/users/orders/products/15
```

Less RESTful:
```
/getUser/createOrder/deleteProduct
```

The action comes from the HTTP method, not the URL.
## Stateless
Each request should contain all the information needed to process it, so we don't need to use additional information stored from previous requests.

The opposite design is the stateful one, where we have a state, which is a stored information used for running the service.

For example, in a stateful design, when using the `GET /orders` endpoint, server might return orders for the currently logged in user (so it uses the state which contains an information about currently logged in user).

Stateless design is beneficial because it:
- Enables horizontal scaling
	- When we create a new instance of a service, we don't need to load the state from the previous instances.
- Makes load balancing simpler
	- In a stateful design, a request must go to the instance that has a proper state (with an information needed) to handle that request
- Avoids server-side session coupling
	- That is avoids a situation where a backend service depends on a stored session state on a specific service instance to understand or continue a user’s interaction.
## HTTP methods and status codes
REST uses HTTP, so that includes methods and status codes ([[Networking - Protocols - HTTP|link]]).
## Uniform interface
One of REST's biggest ideas is that **every resource is accessed in the same way**.

Once a developer understands:
```
GET /users
```

they immediately understand:
```
GET /products
GET /orders
GET /employees
```

The API becomes predictable.
