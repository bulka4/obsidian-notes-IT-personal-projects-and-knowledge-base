Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
A bulk endpoint is an API that allows you to process multiple items in one request instead of one-by-one.

It is used in request batching ([[Backend Engineering - Request batching|link]]) to optimize performance ([[Backend Engineering - Application communication - Performance optimization|link]]) during communication between services.
# Downsides
- partial failures (some succeed, some fail)
- harder validation
- bigger payloads
- more memory usage on server
# Benefits
Making one request instead of multiple ones is better because each network call has overhead:
- connection setup (sometimes)
- request headers
- serialization/deserialization
- latency (biggest cost)