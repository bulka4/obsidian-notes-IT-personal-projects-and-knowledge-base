Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Network partition testing verifies how a distributed system behaves when communication between nodes is interrupted.

A network partition means that nodes are still running, but they cannot communicate with each other.

Tests check:
- Does the system remain available?
- Does it preserve consistency?
- How does it recover after the connection returns?
- Are conflicting updates handled correctly?

Common scenarios:
- database replica loses connection
- Kubernetes nodes cannot communicate
- service-to-service network failure
- message broker connection loss

Techniques:
- block network traffic between services
- add latency
- drop packets
- disconnect nodes temporarily