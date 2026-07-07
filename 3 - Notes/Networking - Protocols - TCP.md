Tags: [[_Networking]]
#Networking 

# Introduction
TCP (Transmission Control Protocol) is a transport-layer protocol that provides reliable, ordered, and error-checked communication between two devices over a network.
# Where TCP fits
TCP is in the transport layer ([[Networking - OSI model|link]]). A simplified network stack looks like:
```
Application  → HTTP
Transport    → TCP
Internet     → IP
Physical     → Ethernet / Wi-Fi
```

So when we make an HTTP request:
```
HTTP
   ↓
TCP
   ↓
IP
   ↓
Internet
```

HTTP defines what we send, while TCP makes sure it arrives reliably.
# Main features of TCP

## 1. Reliable delivery
TCP guarantees that data arrives.

If a packet is lost:
- TCP detects it
- retransmits it
## 2. Ordered delivery
Suppose data is split into packets:
```
Packet 1
Packet 2
Packet 3
```

Even if they arrive as:
```
Packet 3
Packet 1
Packet 2
```

TCP reorders them before giving them to our application.

Our backend simply receives:
```
1 → 2 → 3
```
## 3. Error checking
Each packet contains a checksum.

If corruption is detected:
- packet is discarded
- sender retransmits
## 4. Flow control
Suppose:
- Server can process 1 GB/s
- Client can only process 10 MB/s

TCP prevents overwhelming the slower side by adjusting the sending rate.
## 5. Congestion control
If the network is congested -> TCP slows itself down automatically.

This prevents making congestion even worse.
# TCP is connection-oriented
Before data is sent, TCP establishes a connection.

This happens with the famous three-way handshake:
```
SYN  -------------->
      <------------  SYN-ACK
ACK  -------------->
```

Only after this handshake do they start exchanging application data.
# Closing the connection
When finished:
```
FIN
ACK
FIN
ACK
```

The connection is cleanly terminated.