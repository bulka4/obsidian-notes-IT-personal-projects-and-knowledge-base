Tags: [[_Networking]]
#Networking 

# Introduction
A VPN (Virtual Private Network) creates an encrypted tunnel between two or more networks (or between a device and a network).

Essentially, it makes your computer a member of a remote private network, even if you’re physically somewhere else.

So once connected:

· Your machine gets an internal (private) IP address

· You can communicate with other hosts in that VPN as if you were on the same LAN

· You can resolve and use private DNS names defined in that network

So with VPN we create our own private network. When setting up VPN, we define:

· Private IP range (subnet)

o The internal address space assigned to VPN clients

· DNS server

o Which DNS server clients use

· Domain name

o Your internal domain name for the network

· Hostnames

o Individual machines/services in that network