Tags: [[__My_projects]]
#MyProjects 

# Introduction
This document describes how we could develop this system further.
# Error handling
Error handling - [[Data governance app with a RAG system - Error handling]]
# CQRS
This one is more advanced and **probably shouldn't be implemented just for your project**, but it's an interesting architectural idea to document.

Your system has two very different operations:
```
WRITE:
User → documentation → MongoDB → embedding update

READ:
User → semantic search → vector DB → RAG
```

At larger scale, the read/search representation could be treated as a separate **read model** derived from the source data.

That's conceptually close to **CQRS** and is actually a very natural fit for your RAG system.
# Contract-based communication between services
For your microservices, document defining explicit contracts for communication.

For example:
```
DocumentUpdatedEvent

{
    document_id: 123,
    version: 7,
    timestamp: ...
}
```

Instead of services informally agreeing about what data is sent.

This could eventually lead to schema validation, backward compatibility, and contract testing.
# API versioning
We could version APIs so when we change an API endpoint, we just create a new version for it and existing clients can continue using the old version.

We might have:
```
/api/v1/search
/api/v1/documents
```
and later add another version:
```
/api/v2/search
```
