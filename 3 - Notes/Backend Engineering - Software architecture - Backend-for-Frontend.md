Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Backend-for-Frontend (BFF) is an architectural pattern where each frontend gets its own dedicated backend service tailored to its needs.

Instead of:
```
Mobile App ----\
Web App --------> Shared Backend
Desktop App ----/
```

we have:
```
Mobile App ---> Mobile BFF ---\
                               \
Web App ------> Web BFF --------> Internal Services
                               /
Desktop App --> Desktop BFF --/
```
# Why is it useful?
Different frontends often have different requirements.

Example:
## Mobile app
Needs:
```
- Small payloads
- Few network requests
- Low bandwidth usage
```
## Web application
Needs:
```
- More detailed data
- Different UI composition
```

If both use the same API:
```
GET /user/123
```

then:
- mobile may receive too much data
- web may need multiple additional requests
## Example
Suppose the UI needs:
- user profile
- recent orders
- recommendations

Without BFF:
```
Frontend
   |
   +--> User Service
   +--> Order Service
   +--> Recommendation Service
```

Frontend makes many requests.

With BFF:
```
Frontend
    |
    v
   BFF
    |
    +--> User Service
    +--> Order Service
    +--> Recommendation Service
```

The BFF aggregates everything:
```
{
  "user": {...},
  "orders": [...],
  "recommendations": [...]
}
```

and then BFF makes multiple requests internally and combines the results.

The frontend performs only one request.
# Additional responsibilities of a BFF
A BFF can also:
- aggregate data
- adapt payloads
- handle authentication
- cache responses
- perform frontend-specific business logic
- translate protocols
# Benefits
- Better frontend performance - Fewer network requests.
- Frontend independence - Frontend teams can evolve APIs independently.
- Simpler frontend code - Less orchestration in browsers/mobile apps.
- Hide internal microservices - The frontend does not know about internal service topology.
# Downsides
- More services - increases operational complexity.
- Possible duplication - Some logic may be repeated across BFFs.
# Relationship to API Gateway
These are different concepts.
## API Gateway
Usually handles cross-cutting concerns:
- routing
- authentication
- rate limiting
- logging

More info - [[Backend Engineering - API architectures - API gateway|link]].
## BFF
Focuses on:
- frontend-specific APIs
- response composition
- frontend needs

Often:
```
Frontend
     |
API Gateway
     |
    BFF
     |
Microservices
```
# When is BFF useful?
Particularly when:
- there are multiple frontends
- frontends have very different requirements
- there are many microservices
- reducing frontend complexity is important