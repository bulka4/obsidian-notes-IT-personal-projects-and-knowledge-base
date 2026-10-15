Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
**API versioning** is the practice of allowing an API to evolve without unexpectedly breaking clients that depend on its existing contract.

The key idea is:
> A client should be able to continue using an older API contract while the server evolves.

When we want to change an API, instead of creating a new one and deleting the old one, we keep the old one and create a new one as a new version.