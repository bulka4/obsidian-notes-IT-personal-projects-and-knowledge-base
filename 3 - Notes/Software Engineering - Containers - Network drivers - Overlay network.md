Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Creates a network spanning multiple Docker hosts.
```
Host 1                 Host 2

Container A            Container B
    |                      |
    +------ overlay -------+
           network
```
Containers can communicate as if they are on the same network.

Used for:
- Docker Swarm
- distributed applications

Kubernetes uses a similar concept through CNI network plugins.