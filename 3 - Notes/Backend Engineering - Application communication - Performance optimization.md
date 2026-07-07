Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
You should always think:
- Network is slower than code
- Serialization costs matter
- Chatty APIs are bad (too many small calls instead of fewer bigger ones)

Key optimizations:
- batching requests - [[Backend Engineering - Request batching|link]] 
- caching (Redis, CDN) - [[Backend Engineering - Caching|link]] 
- reducing payload size (amount of data sent over a network when sending requests / responses)