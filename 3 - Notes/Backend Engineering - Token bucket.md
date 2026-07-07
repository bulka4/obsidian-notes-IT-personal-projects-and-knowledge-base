Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Token bucket is a technique for implementing rate limiting ([[Backend Engineering - Rate limiting|link]]):
- We create for a user a bucket which contains tokens
- Every time a user makes a request, they use one token
- Every second, one token is added to the bucket

So user can me maximally x requests at once, where x is a number of tokens in a bucket, and after some time they are allowed to send new requests.