Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
SASL (Simple Authentication and Security Layer) is a framework that allows a client and a server to authenticate each other using different authentication mechanisms.
# How it works
1. The client connects to a server.
2. The server and client select a SASL authentication mechanism.
3. They exchange the messages required by that mechanism.
4. The server determines whether authentication succeeds.
# Common SASL mechanisms
- **PLAIN**: Sends a username and password in a simple format. It should be protected by TLS because the credentials aren't encrypted by SASL itself.
- **SCRAM**: Uses a challenge-response process based on a password, avoiding transmission of the password itself.
- **GSSAPI**: Commonly used with Kerberos for ticket-based authentication.