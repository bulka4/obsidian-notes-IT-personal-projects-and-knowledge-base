Tags: [[__Web_Development]]
#WebDevelopment 

# Introduction
Reverse proxy is a bridge between a client and an ASGI server ([[ASGI server|link]]), client talks to a reverse proxy and reverse proxy talks to ASGI server:
```python
Client <-> Reverse Proxy <-> ASGI Server
```

It is used in communication in both ways:
- When client sends a request to the server
- When server sends back a response

Reverse proxy is used for:
- Using HTTPS/TLS (security)
- Load balancing 
- Applies policies:
	- Rate limits
	- IP allow/deny
	- Timeouts
	- Headers
- 