Tags: [[_Software_Engineering]]
#SoftwareEngineering 

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
# Combining multiple requests
BFF can be also used to combine multiple requests into a single one. So instead for one frontend to make requests to a few services, for example:
- User Service
- Order Service
- Recommendation Service

it can make one request to BFF and BFF will handle those multiple requests instead of frontend:
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

The BFF aggregates data from all the requests:
```json
{
  "user": {...},
  "orders": [...],
  "recommendations": [...]
}
```

and then BFF makes multiple requests internally and combines the results.

The frontend performs only one request.
# Example
## Mobile vs web app
- Mobile app needs:
```
- Small payloads
- Few network requests
- Low bandwidth usage
```

- Web application needs:
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
- web may need multiple additional requests to get all the data needed
# Additional responsibilities of a BFF
A BFF can also:
- aggregate data:
	- Combine data from multiple services into one response
	- Transform data into a UI-friendly format
	- Remove unnecessary fields
	- Compute derived values (totals, statuses, counts)
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
- Different frontends often have different requirements so we can optimize each backend for each frontend.
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