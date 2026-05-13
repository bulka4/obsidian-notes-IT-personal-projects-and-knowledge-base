Tags: [[_Networking]]
#Networking 

# Introduction
DNS is a server used for translating domain names and hostnames (or in short DNS names) into IP addresses and vice versa.

Domain is a name that identifies a website / organization. So domain includes a group of servers.

It consists of multiple levels:
- Subdomain
- Second level domain
- Top level domain

So the entire domain is written as:
> `<subdomain>.<second-level-domain>.<top-level-domain>`

Every level narrows down a group of servers which belongs to this level. So servers are grouped this way:
- Some group of servers belong to the top level domain
- A part of servers from the top level domain belongs to the second level domain
- A part of servers from the second level domain belongs to the subdomain

Hostname is a name that identifies a specific server within a domain.

Within the same domain each server must have a unique hostname.

If servers are from different domains then they can have the same hostname.

FQDN is a name that includes a hostname and all domain levels:
> `<hostname>.<subdomain>.<second-level-domain>.<top-level-domain>`

FQDN uniquely identifies each server within a network.

`/etc/resolv.conf` file contains information about IP addresses of the DNS servers which are used for translating DNS names.

In the `resolv.conf` file there might be written:
- search domain-name-1 domain-name-2 …
- Options ndots:x

That means there need to be at least x dots in the domain name in order to be treated as FQDN.

So if host tries to resolve a domain name which has less than x dots, then it will try to append domain names from the ‘search’ field to the domain name which it is trying to resolve.

There might be a situation that host will try to use only the first domain name from the ‘search’ field and if it fails it will not try other names.