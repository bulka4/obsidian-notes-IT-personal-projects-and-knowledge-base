Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
HTTP chunked transfer encoding is a way for a server to send a response in pieces (chunks) instead of one big payload.

Instead of waiting to send the full response:
> server streams the response in small chunks as it generates them

So:
- no fixed `Content-Length` required upfront
- data is sent progressively
# How it works
A response is split like this:
```
chunk 1
chunk 2
chunk 3
...
0 (end)
```

Each chunk is sent immediately when ready, and the connection stays open until the final `0` chunk signals completion.
# Why it exists
Normally HTTP expects:
- “here is the full response size” → then send everything

But chunked transfer solves:
- slow generation (big files, streaming results)
- unknown total size in advance
# Key characteristics
## 1. Streaming over HTTP
- response is delivered incrementally
- client can start processing early
## 2. No known final size
- server does NOT need to compute total length first
## 3. Still request → response model
Even though it streams:
> it is still a single HTTP response, just delivered gradually
## 4. Data format
HTTP chunked transfer can send data in any format. It is not structured like in SSE ([[Backend Engineering - Streaming API Architecture - Server-Sent Events (SSE)|link]]).
# Example use cases
- large file downloads (generated on the fly)
- log streaming
- AI model token streaming
- long-running computations
- proxies / gateways streaming upstream responses
