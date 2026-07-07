Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Token-based authentication is a common way to implement authentication and authorization in stateless ([[Backend Engineering - Stateful vs stateless service|link]]) backend systems.

In this method, a server gives a token to a client after login, and the client sends it with every request to prove who they are.

This token can be for example in the JWT format ([[Backend Engineering - Security - JWT access token format|link]]).
# What problem it solves
Without a token:
- server must store sessions (stateful)
- hard to scale across multiple servers

With JWT:
> the client carries its own identity in a signed token (stateless)
# How it works
- Client logs in and server returns a token
- Client stores token memory or `localStorage` (web)
- Client sends token with requests:
  ```
	GET /orders
	Authorization: Bearer <token>
  ```
- Server verifies the token
# Important features
## Token expiration matters
Always use expiration time to limit token lifetime.
## Revocation is tricky
Because JWT is stateless, we can’t easily “delete” a token unless we:
- use short expiration times
- maintain a blacklist (optional - list of tokens which can't be used for authentication)