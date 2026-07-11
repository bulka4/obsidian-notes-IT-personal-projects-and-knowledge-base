Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
SOAP (Simple Object Access Protocol) is a protocol for communication between applications, especially web services.

SOAP defines:
- message format (XML)
- error handling
- service description
- communication rules
# SOAP message format
SOAP messages are XML documents.

Example request:
```xml
<soap:Envelope>
    <soap:Body>
        <GetUser>
            <id>123</id>
        </GetUser>
    </soap:Body>
</soap:Envelope>
```

Response:
```xml
<soap:Envelope>
    <soap:Body>
        <GetUserResponse>
            <name>Alice</name>
        </GetUserResponse>
    </soap:Body>
</soap:Envelope>
```

Everything is wrapped inside a SOAP Envelope.
# Main components
## 1. Envelope
Defines the SOAP message.
## 2. Header (optional)
Contains metadata:
- authentication
- transactions
- routing information
## 3. Body
Contains the actual request or response.
## 4. Fault
Standardized error format.

Example:
```xml
<soap:Fault>
    <faultcode>Client</faultcode>
    <faultstring>User not found</faultstring>
</soap:Fault>
```
# WSDL
SOAP services are often described using WSDL (Web Services Description Language).

A WSDL file defines:
- available operations
- parameters
- return types
- endpoints

It is basically a formal API contract. Tools can even generate client code automatically.
# Transport protocol
SOAP most commonly uses HTTP but unlike REST, SOAP is not tied to HTTP. It can also use:
- SMTP
- TCP
- message queues
# Why SOAP became less popular
SOAP messages can become quite verbose. For example:

SOAP:
```xml
<soap:Envelope>
   ...
      <GetUser>
         <id>123</id>
      </GetUser>
   ...
</soap:Envelope>
```

REST:
```json
{
  "id": 123
}
```

REST with JSON is usually:
- simpler
- easier to debug
- smaller over the network
# Why SOAP is still used
SOAP remains common in industries requiring strong standards:
- banking
- insurance
- telecom
- government systems
- enterprise integration

because SOAP provides standards such as:
- WS-Security
- transactions
- reliable messaging
# WS-Security
Provides standardized security mechanisms for SOAP messages.

Features:
- authentication
- message integrity
- encryption

Unlike HTTPS, which secures the connection, WS-Security secures the message itself.

This is useful when a message passes through multiple intermediaries:
```
Client → Gateway → Queue → Service
```

The message can remain signed and encrypted end-to-end.

Typical features:
- Username/password tokens
- X.509 certificates
- XML signatures
- XML encryption
# Transactions (WS-Transaction)
Extends the idea of database transactions across multiple services.

Example:
```
Book flight
Book hotel
Charge credit card
```

We may want:
```
All succeed
OR
All fail
```

Similar to ACID transactions.

Example:
```
Service A: reserve item
Service B: process payment
Service C: create shipment
```

If shipment fails:
```
Undo payment
Undo reservation
```

This is called a distributed transaction.

SOAP had standards for coordinating such workflows.
# Reliable Messaging (WS-ReliableMessaging)
Ensures messages are delivered reliably.

Normal HTTP:
```
Client → Server

What if network fails?
```

You may not know whether:
- the message was delivered
- it was processed
- it was lost

Reliable messaging adds guarantees like:
- message acknowledgement
- retries
- duplicate detection
- ordering

Example:
```
Message #1
Message #2
Message #3
```

The protocol ensures:
```
1 → 2 → 3
```

even if packets are lost or reordered.

This is useful for:
- financial systems
- order processing
- enterprise integrations

where losing a message is unacceptable.