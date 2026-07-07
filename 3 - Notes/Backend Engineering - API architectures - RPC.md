Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
RPC (Remote Procedure Call) is an API architectural style where we design distributed systems as if we are calling functions or methods on another machine.

So instead of thinking in terms of resources (like in REST) or queries (like in GraphQL), we think in terms of functions / actions, for example:
- `createUser(name, email)`
- `getUser(id)`
- `predict(features)`
- `trainModel(config)`

From the developer’s perspective, it feels like a local function call.
# Key characteristics
## 1. Action-oriented
- Focus is on **what you do**, not what resource you manipulate
- Example: `chargeCard()` instead of `POST /payments`
## 2. Tight coupling of interface
- Client and server must agree on:
    - method names
    - input/output structure
- Usually defined via an **IDL (Interface Definition Language)**
## 3. Strong contract (often)
- In modern RPC (like gRPC), schemas are strictly defined
- This enables:
    - code generation
    - type safety
    - performance optimization
## 4. Less “self-descriptive” than REST
- REST uses HTTP verbs + URLs meaningfully
- RPC is more like calling private APIs:
    - `doThingX()`
    - `runJob()`
# Common forms of RPC
## 1. Classic RPC (conceptual model)
- General distributed systems idea
- Not tied to a specific tech
## 2. JSON-RPC
- Lightweight RPC over HTTP
- Uses JSON messages
## 3. gRPC (modern RPC system)
- More info - [[Networking - Protocols - gRPC|link]] 
- Uses HTTP/2 + Protobuf
- High performance
- Streaming support
- Widely used in microservices