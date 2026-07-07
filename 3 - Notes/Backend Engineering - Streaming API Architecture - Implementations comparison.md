Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction

| Feature                 | WebSockets                  | SSE                                    | Chunked HTTP                          | gRPC Streaming                                        |
| ----------------------- | --------------------------- | -------------------------------------- | ------------------------------------- | ----------------------------------------------------- |
| Type                    | Protocol                    | Streaming mechanism over HTTP          | HTTP transfer encoding                | RPC framework (built on HTTP/2)                       |
| Communication direction | Bidirectional               | Server -> client                       | Usually server -> client              | Uni or bidirectional                                  |
| Streaming support       | yes (native frames)         | yes (event stream)                     | yes (raw bytes)                       | yes (structures messages)                             |
| message structure       | Frames (binary/text)        | event-based(data and event attributes) | none (raw bytes)                      | Strongly typed protobuf messages                      |
| State model             | Stateful connection         | Stateful connection                    | Stateless HTTP response stream        | Stateful streaming RPC call                           |
| Transport               | WebSocket protocol over TCP | HTTP/1.1 or HTTP/2                     | HTTP/1.1 or HTTP/2                    | HTTP/2                                                |
| Browser support         | Native WebSocket API        | Native EventSource API                 | Fetch streaming (manual)              | No native browser support (needs client lib)          |
| Complexity              | Medium                      | Low                                    | Low-Medium                            | High                                                  |
| Performance efficiency  | High                        | Medium                                 | Medium                                | Very high                                             |
| Backpressure handling   | yes                         | limited                                | manual                                | Built-in (HTTP/2 flow control)                        |
| Reconnection support    | manual                      | automatic                              | manual                                | Built-in at transport level (varies by client)        |
| Best use cases          | Chat, games, collaboration  | Notifications, live feeds, AI tokens   | File streaming, proxying, raw streams | Microservices, ML systems, high-performance pipelines |
| Data format constraint  | Any (binary/text)           | text                                   | any bytes                             | strong schema (protobuf)                              |
