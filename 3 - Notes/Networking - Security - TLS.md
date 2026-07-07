Tags: [[_Networking]]
#Networking  

# Introduction
TLS (Transport Layer Security) is a cryptographic protocol that provides secure communication over a network.

When we send data over a network using TLS, this data is encrypted so even if someone catches it, they can't understand it.

Its job is to make sure:
- **privacy** → no one can read your data
- **integrity** → no one can change your data
- **authentication** → you’re talking to the real server

It is a security layer on top of TCP ([[Networking - Protocols - TCP|link]]) so it is mainly used with TCP but it can be used with other protocols as well, for example QUIC.
# How TLS works
When we send data (like login info or API requests), TLS:
## 1. Encrypts data
So even if someone intercepts it, they see nonsense:
```
Hello → 8x$kL@91!!
```
## 2. Ensures integrity
Detects if data was modified in transit.
## 3. Verifies identity
Checks the server is legitimate using certificates.
# Connecting using TLS
When a client connects to a server using TLS, then the following process is followed:
## Step 1: Transport connection (or transport context)
The client establishes a connection using a transport protocol (commonly TCP, but could also be QUIC or another transport).
## Step 2: TLS handshake starts
Client and server begin the TLS handshake to negotiate security parameters.

They agree on:
- TLS version (e.g., TLS 1.3)
- encryption algorithms (cipher suites)
- key exchange method
## Step 3: Server authentication (certificate)
The server presents a **TLS certificate** proving its identity.

The client verifies:
- certificate is issued by a trusted Certificate Authority (CA)
- certificate is not expired
- certificate matches the expected domain/identity
## Step 4: Key exchange
Client and server securely generate or exchange material to derive a **shared secret key**.

This key will be used for symmetric encryption.
## Step 5: Secure channel established
Both sides now have the same shared secret.

From this point on:
- all application data is encrypted
- data integrity is protected
- communication is authenticated
# TLS handshake (simple view)
```
Client → "Hello, I support TLS versions X"
Server → "Here is my certificate"
Client → "Certificate OK, here is key info"
Both  → "We now share a secret key"
```

After this all communication is encrypted using that shared key.
# Why certificates matter
A TLS certificate is like a digital passport for a website.

It contains:
- domain name (example.com)
- public key
- issuer (Certificate Authority)
- expiration date

If a fake server tries to impersonate Google:
- browser will detect invalid certificate
- connection will be blocked or warned
# Protocols we can use TLS with
We can use TLS together with different protocols, for example:
- HTTP (i.e. HTTPS ([[Networking - Security - HTTPS|link]]))
- SMTP (email)
- FTP
- gRPC
- APIs