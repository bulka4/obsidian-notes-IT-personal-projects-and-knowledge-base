Tags: [[_Networking]]
#Networking 

# Introduction

A proxy is a system that acts as a intermediary between a client and another server. So communication works like that:

Client => Proxy => Server

## Forward proxy

A forward proxy is used in a communication between a client and the internet:

Client => Proxy => Internet

It hides the **client’s** identity.

Common uses:

· Bypass geo-blocking

· Content filtering

· Security/firewall

## Reverse proxy

A reverse proxy is used in a communication between the internet and internal servers:

Internet => Proxy => Internal Servers

It hides the **server’s** identity.

Common uses:

· Load balancing

· SSL termination

· Caching (e.g., for web apps)

· Rate limiting / DDoS protection