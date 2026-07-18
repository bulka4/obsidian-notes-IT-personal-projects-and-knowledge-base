Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
API integration tests verify that:
- our application correctly interacts with APIs 
- or that other applications correctly interacts with the API that we created

usually using a real HTTP communication and multiple components together.

They test the entire process of handling a request:
```
Client
   |
HTTP
   |
API
   |
Database / Services
```
rather than testing individual functions in isolation like unit tests.
# What to test
We make a request and check whether:
- We receive a correct status code and message in a response
- JSON returned as a response is correct - fields exist, field types are correct, serialization works
- Correct records were created in a database
- We get correct errors when making an incorrect request
- Authentication and authorization works correctly
# Difference from E2E tests
API integration tests usually stop at the backend. E2E tests also include frontend, for example we make some action using front end (e.g. click a button) and check whether the result is correct.
# What bugs do they catch?
Examples:
- wrong routing
- incorrect JSON serialization
- broken validation
- dependency injection issues
- database configuration issues
- authentication bugs
- API contract changes
# Typical tools
- Java: Spring Boot Test, `Testcontainers`
- Python: `pytest` + `requests`/`FastAPI` test client
- C++: custom HTTP clients, integration frameworks