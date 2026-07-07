Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Streaming / Real-time API Architecture is an API style where instead of making one request and getting one response, the client and server exchange continuous data over time.
# Key characteristics
## 1. Persistent communication
- Connection stays open
- Data flows over time instead of a single payload
## 2. Incremental delivery
Instead of waiting for full results:
- server sends partial updates
- client processes data as it arrives

Example:
- live stock prices
- AI token-by-token output
- log streaming
- sensor data feeds
## 3. Low latency experience
- user sees results immediately
- no need to wait for full computation
# Types of streaming API architectures
## 1. Server → Client streaming (most common)
Server continuously pushes data to client.

Examples:
- live dashboards
- AI response streaming
- notifications feed
## 2. Client → Server streaming
Client sends continuous data stream.

Examples:
- uploading video in chunks
- telemetry / IoT data ingestion
## 3. Bidirectional streaming
Both sides send data continuously.

Examples:
- chat systems
- multiplayer games
- collaborative tools
# Common architectural implementations (conceptually)
These are mechanisms, not the architecture itself:
- WebSockets (bidirectional real-time channel, [[Networking - Protocols - WebSockets|link]])
- Server-Sent Events (server → client streaming over HTTP, [[Backend Engineering - Streaming API Architecture - Server-Sent Events (SSE)|link]])
- Chunked HTTP (streaming responses, [[Backend Engineering - Streaming API Architecture - Chunked HTTP|link]])
- gRPC streaming (structured RPC-based streaming, [[Backend Engineering - Streaming API Architecture - gRPC streaming|link]])
# Implementations comparison
[[Backend Engineering - Streaming API Architecture - Implementations comparison]]