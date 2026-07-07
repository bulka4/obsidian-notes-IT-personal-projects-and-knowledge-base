Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
gRPC streaming is an extension of gRPC (RPC architecture) where instead of a single request → single response, you get a continuous stream of messages between client and server.

It keeps the RPC “function call” model, but adds streaming as a first-class feature.

Normal gRPC:
> `GetUser(id) → User`

gRPC streaming:
> `streamPredict(inputs) → stream of predictions over time`

So instead of one return value, you get **many messages over a live connection**.
# 3 types of gRPC streaming
## 1. Server-side streaming
Client sends **one request**, server sends **many responses**

Example:
- model training progress
- LLM token streaming
- log streaming
```
Client → Server: request
Server → Client: response1
Server → Client: response2
Server → Client: response3
...
```
## 2. Client-side streaming
Client sends **many requests**, server returns **one response**

Example:
- uploading chunks of a file
- sending sensor data batch
```
Client → Server: chunk1
Client → Server: chunk2
Client → Server: chunk3
Server → Client: final result
```
## 3. Bidirectional streaming
Both sides send streams independently

Example:
- chat systems
- multiplayer games
- real-time collaboration
```
Client ↔ Server (both continuously sending messages)
```
# Key features
## 1. Structured contract (big difference)
gRPC uses a strict schema via `.proto`:
```
service ModelService {
  rpc PredictStream (Input) returns (stream Output);
}
```

So:
- message types are strongly defined
- both sides know exact structure
## 2. Runs over HTTP/2
This gives:
- multiplexing (many streams over one connection)
- flow control
- low latency framing
## 3. Binary format (Protocol Buffers)
Instead of text:
- compact
- fast
- efficient for ML / high-throughput systems
# When gRPC streaming is used
## 1. ML / AI systems
- token streaming from LLMs
- inference streams
- training progress updates
## 2. Microservices pipelines
- data processing pipelines
- ETL flows
- event processing
## 3. High-performance real-time systems
- trading systems
- telemetry ingestion
- internal service communication