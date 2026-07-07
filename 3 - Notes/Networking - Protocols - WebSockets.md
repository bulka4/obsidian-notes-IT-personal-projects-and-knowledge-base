Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
WebSockets are a way for a client and server to keep a **continuous, two-way communication channel** open over a single connection.

Unlike HTTP (where you request → get response → connection ends), connection in WebSockets stays open.
# How it starts
We start a connection using a HTTP protocol and then connection switches protocol to a websocket.
# Stateful connection
A websocket connection is stateful as it needs to remember information about the connection while it stays open. Information like:
- who the user is
- that the connection is still alive
- what session it belongs to
- what data has already been sent/received
# Benefits
1. Full duplex - Both sides can talk simultaneously.
2. Persistent connection - One connection stays open for minutes/hours.
3. Low latency - No repeated HTTP setup overhead.
4. Lightweight messages - No full HTTP headers each time.
# Drawbacks
1. Expensive - Connection stays open for longer time what takes more resources
2. Load balancing and horizontal scaling are harder - If one server gets overloaded, we can't simply move connections to other servers. We need to close connections, reopen them and restore state what is complex.
3. Stateful servers - WebSocket servers are often stateful, because they must remember active connections and user sessions are tied to memory
4. Reconnection is harder - We need to handle reconnect logic, message replay, missed messages, resynchronization
# When to use it
It is good when we need to send requests multiple times over a short period, e.g. in chats, multi-player games, trading systems, live dashboards.
# Questions
- Why load balancing is harder? Because some connections can stay open for longer and some for shorter?
# Other notes
- Persistent bi-directional connection
- Used for real-time systems (chat, trading, dashboards)