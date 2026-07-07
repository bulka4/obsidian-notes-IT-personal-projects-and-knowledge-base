Tags: [[_Networking]]
#Networking 

# Introduction
UDP (User Datagram Protocol) is a transport-layer protocol that provides fast, lightweight communication between two devices.

Unlike TCP, UDP **does not guarantee** that data arrives, arrives in order, or arrives only once.

Its philosophy is:
> "Send the data as quickly as possible and don't wait for confirmation."
# Where UDP fits
UDP is in the transport layer ([[Networking - OSI model|link]]), just like TCP. It sits below application protocols:
```
Application  → DNS, VoIP, Online Games, Streaming
Transport    → UDP
Internet     → IP
Physical     → Ethernet / Wi-Fi
```

So an application sends data to UDP, which sends it over IP.
# What UDP does (and doesn't) do
Suppose we send:
```
Hello World
```

UDP simply sends it.

It does not:
- check if it arrived
- resend lost packets
- reorder packets
- establish a connection first

This makes it much faster than TCP.
# Main features of UDP
# 1. Connectionless
There is no handshake.

TCP:
```
Handshake
↓
Send data
```

UDP:
```
Send data immediately
```
## 2. No reliability
If a packet is lost:
```
Packet 1
Packet 2   ← lost
Packet 3
```

UDP doesn't care.

The application decides what to do.
## 3. No ordering
Packets may arrive:
```
312
```

UDP delivers them exactly as they arrive.
## 4. Very low overhead
Because UDP doesn't:
- establish connections
- retransmit
- track packet order
- manage congestion like TCP

it is extremely lightweight.
# When to use it
Sometimes speed is more important than perfection. For example:
## Video streaming
Examples:
- Zoom
- Google Meet
- Discord

Small packet loss is acceptable (e.g. one frame is lost).

Low latency is much more important.
## Online games
Player position updates:
```
Player X = (100, 250)
```

If one update is lost, the next one arrives milliseconds later.

No reason to retransmit old positions.
## Live audio
For voice chat, losing one word is usually better than introducing noticeable delay.