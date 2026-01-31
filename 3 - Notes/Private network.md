Tags: [[_Networking]]
#Networking

# Introduction
In a private network servers have assigned private IPs, there are not public ones. 

Public IPs can be seen by other servers over a public internet, private ones can't. That means, that servers in a private networks can't be reached from outside of that private network at all. Even if someone guess the private IP of the server, they will not be able to reach it.

Private network can be created cloud services, like Azure VNet, and to access it from a server from outside of that network, we can use VPN.
# Predictable IPs
In a private network, servers get assigned predictable IPs (from specified ranges). Thanks to that, it is easier to control traffic and identify servers.

For example, we can have two groups of servers and each one get assigned a different IP range:
- `10.0.1.x`
- `10.0.2.x`
if we see an IP like `10.0.1.12`, we know that it belongs to one of the servers from the IP range `10.0.1.x`.