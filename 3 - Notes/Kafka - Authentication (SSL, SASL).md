Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Authentication verifies the identity of clients and brokers connecting to Kafka.
# SSL/TLS authentication (certificates)
The client proves its identity using a digital certificate (TLS - [[Networking - Security - TLS|link]]).

Example:
```
Producer
   |
   | sends certificate
   v
Kafka broker
   |
   | verifies certificate
   v
Connection allowed
```

Often used for:
- strong identity verification
- encrypting communication (TLS also provides encryption)
# SASL (Simple Authentication and Security Layer)
SASL ([[Backend Engineering - Security - SASL (Simple Authentication and Security Layer)|link]]) is a framework that supports different authentication methods.

Examples:
- SASL/PLAIN → username + password
- SASL/SCRAM → username + password with stronger hashing
- SASL/GSSAPI (Kerberos) → enterprise authentication

Example:
```
Producer
   |
   | username + password/token
   v
Kafka broker
   |
   | verifies credentials
   v
Connection allowed
```