Tags: [[_Networking]]
#Networking 

# Introduction
A proxy is a system that acts as a intermediary between a client and another server. So communication works like that:
```
Client => Proxy => Server
```
# Forward proxy
A forward proxy is used in a communication between a client and the internet:
```
Client => Forward proxy => Internet
```

It hides the client’s identity.
## Use cases
Common use cases:
### Security filtering
- Block malicious websites
- Scan downloads for malware
- Prevent employees from accessing certain resources
### Anonymity / hiding clients
Websites see the proxy's IP instead of the user's IP
### Centralized internet access
A company can enforce rules:
```
All employees → company proxy → Internet
```
### Caching
Frequently accessed resources can be stored locally:
```
Employee A downloads file
Employee B requests same file
	   |
	   v
Proxy serves cached copy
```
# Reverse proxy
A reverse proxy is used in a communication between the internet and internal servers:
```
Internet => Reverse proxy => Internal Servers
```

It hides the server’s identity.
## Use cases
Common use cases:
### Hide internal servers
  Users see:
```
example.com
```

but internally:
```
example.com
	   |
	   v
Reverse proxy
	   |
	   +--> server 1
	   +--> server 2
	   +--> server 3
```

The client never know the real servers.
### Load balancing
Distribute requests:
```
			 Reverse proxy
				  |
	   ---------------------
	   |         |         |
	Server1   Server2   Server3
```

Without it, all users might hit one server.
### TLS termination
Instead of every application server handling HTTPS:
```
Client
 HTTPS
  |
  v
Reverse proxy
  |
 HTTP/internal TLS
  |
  v
Servers
```
### Protection against attacks
A reverse proxy can:
- block suspicious IPs
- limit request rates
- filter malicious requests
- hide server IP addresses

Example:
```
Attacker
   |
   v
Reverse proxy
   |
(blocked)
```

The proxy manages certificates and encryption.
### Others
- Caching (e.g., for web apps)
- Rate limiting / DDoS protection