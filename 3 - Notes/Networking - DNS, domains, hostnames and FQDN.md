Tags: [[_Networking]]
#Networking 

# DNS
DNS (Domain Name System) is a system that translates domain names/hostnames (DNS names) into IP addresses and other records (and sometimes performs reverse lookup from IP addresses to names).

DNS consists of many servers:
- root DNS servers
- TLD DNS servers
- authoritative DNS servers
- recursive resolvers
# Domain
A domain is a name that identifies a website / organization, for example `api.myapplication.com`. It can have zero, one, or many servers associated with it.

It consists of multiple levels:
- Subdomain (optional)
- Second level domain
- Top level domain

So the entire domain is written as:
> `<subdomain>.<second-level-domain>.<top-level-domain>`

Every level narrows down a group of servers which this level points to. So servers are grouped this way:
- Some group of servers are pointed to by the top level domain
- A part of servers from the top level domain are pointed to by to the second level domain
- A part of servers from the second level domain are pointed to by to the subdomain
# Hostname
Hostname is a name that identifies a specific host within a domain where a host can be:
- physical server
- VM
- container (sometimes)
- network appliance

Additionally:
- Within the same domain each host must have a unique hostname.
- If host are from different domains then they can have the same hostname.
# FQDN
FQDN is a name that includes a hostname and all domain levels:
> `<hostname>.<subdomain>.<second-level-domain>.<top-level-domain>`

FQDN uniquely identifies each hostname in the DNS namespace.
# `resolv.conf`
`/etc/resolv.conf` file contains information about IP addresses of the DNS servers which are used for translating DNS names.

In the `resolv.conf` file there might be written:
- `search domain-name-1 domain-name-2 …`
- `Options ndots:x`

That means there need to be at least x dots in the domain name in order to be treated as FQDN.

So if host tries to resolve a domain name which has less than x dots, then it will try to append domain names from the ‘search’ field to the domain name which it is trying to resolve.

There might be a situation that host will try to use only the first domain name from the ‘search’ field and if it fails it will not try other names.