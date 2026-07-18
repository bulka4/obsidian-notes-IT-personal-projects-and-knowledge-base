Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
SASL (Simple Authentication and Security Layer) is a framework for authentication — it defines how a client proves its identity to a server.

It does not primarily provide encryption (TLS does that).

Example:
```
Client
   |
   | "I am user X"
   | credentials/token
   v
Server
   |
   | verifies identity
   v
Access granted
```

Common SASL mechanisms:
- SASL/PLAIN → username + password (simple, usually combined with TLS)
- SASL/SCRAM → username + password with secure challenge-response
- SASL/GSSAPI (Kerberos) → enterprise authentication
- SASL/OAUTHBEARER → OAuth tokens