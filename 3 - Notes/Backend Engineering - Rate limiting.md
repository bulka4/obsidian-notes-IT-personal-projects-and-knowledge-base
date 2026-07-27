Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Rate limiting is a technique for limiting how many requests a client is allowed to make. For example, 100 requests per minute per API key ([[Backend Engineering - Security - API key|link]]).

If someone sends more requests than the allowed limit, the server sends response `429 Too many requests`.
# Storing information about number of requests made by users
For example Redis database can be used to store information about how many requests each user has already made.

It can be a shared database used by many Kubernetes pods running application.
# Techniques for implementing rate limiting
- Token bucket - [[Backend Engineering - Token bucket|link]] 
- Circuit braker - [[Software Engineering - Fault tolerance - Circuit breakers|link]] 
