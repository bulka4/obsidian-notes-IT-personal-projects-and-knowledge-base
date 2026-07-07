Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Server-Sent Events (SSE) is a real-time streaming API pattern where the server pushes updates to the client over a single long-lived HTTP connection.

Instead of:
- client repeatedly asking: “anything new?” (polling)

SSE does:
> client opens connection once → server keeps sending updates forever (or until closed)

So it’s:
> server → client one-way streaming over HTTP
# How it works
1. Client sends a normal HTTP request:
    - `GET /events`
2. Server responds **but does NOT close the connection**
3. Server continuously sends messages like:
    ```
    data: new update 1data: new update 2data: new update 3
    ```
4. Client listens and processes events as they arrive
# Key characteristics
## 1. One-way communication
- Only **server → client**
- Client cannot send data on the same channel (must use normal HTTP requests separately)
## 2. Built on HTTP
- No special protocol required
- Uses standard HTTP/1.1 or HTTP/2
- Much simpler than WebSockets
## 3. Automatic reconnection
- Browser automatically reconnects if connection drops
- Can resume using “last event ID” (optional feature)
## 4. Lightweight
- No binary framing or complex protocol
- Just plain text stream (`text/event-stream`)
# Event format
SSE sends structured text events:
```
event: message
id: 42
data: Hello world
```

Fields:
- `data:` → payload (main content)
- `event:` → event type (optional)
- `id:` → event identifier (for resuming)
- blank line → end of event
# Client-side usage (browser)
```javascript
const es = new EventSource("/events");

es.onmessage = (event) => {
  console.log("New data:", event.data);
};
```

Or for named events:
```javascript
es.addEventListener("message", (e) => {
  console.log(e.data);
});
```
# When SSE is a great fit
## 1. Live updates
- notifications
- dashboards
- monitoring systems
## 2. Streaming AI responses
- LLM token streaming (very common)
- progress updates for long tasks
## 3. Event feeds
- activity streams (GitHub-like feeds)
- logs / telemetry
# Comparison to WebSockets
WebSockets are for bidirectional communication - both sides can exchange messages all the time when a connection is open.

SSE is used only for a server to send messages to the client who sent a request.