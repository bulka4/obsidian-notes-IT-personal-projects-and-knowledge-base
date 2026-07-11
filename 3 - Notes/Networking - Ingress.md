Tags: [[_Networking]]
#Networking 

# Introduction
Ingress is a rule/configuration that tells a system how external HTTP/HTTPS traffic should reach internal services.

It belongs to the Layer 7 of the OSI model ([[Networking - OSI model|link]]).
# What problem does it solve
Without ingress, each service needs its own external endpoint (domain ([[Networking - DNS, domains, hostnames and FQDN|link]])):
```
Internet
   |
   +--> Service A (A.example.com)
   |
   +--> Service B (B.example.com)
   |
   +--> Service C (C.example.com)
```

With ingress:
```
Internet
   |
   v
example.com
   |
   v
Ingress
   |
   +--> example.com/api     -> backend service
   |
   +--> example.com/users   -> user service
   |
   +--> example.com/shop    -> shopping service
```
# Example
We might define:
```
api.example.com
        |
        v
   API service

app.example.com
        |
        v
   Frontend service

example.com/admin
        |
        v
   Admin service
```

The Ingress controller reads these rules and acts like a reverse proxy ([[Networking - Proxy (forward, reverse)|link]]).