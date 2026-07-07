Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
An API gateway is a component that sits in front of our backend services and acts as a single entry point for all client requests.

The workflow is like this:
- A client sends requests to the API gateway
- API gateway send another requests to other services
- Services process requests and send back responses to the API gateway
- API gateway sends the final response to the client
# Benefits
## Authentication and authorization
API gateway can:
- Check JWT / OAuth tokens
- Verify identity before forwarding request
- Block access to certain routes (endpoints)
## Rate limiting
We can use rate limiting ([[Backend Engineering - Rate limiting|link]]) in an API gateway to prevent abuse (sending too many requests in a specific time frame by a client).
## Input validation / request filtering
- Reject malformed requests early
- Block suspicious payloads
## TLS termination
API gateway often handles:
- HTTPS encryption/decryption
- certificate management

So backend services can use plain internal traffic (without TLS which is faster and easier).
## Logging & monitoring
- logs all incoming requests
- tracks metrics (latency, errors)
- provides audit trails