Tags: [[__DevOps]], [[__Infrastructure_Engineering]]

# Introduction
Docker container has a separate network namespace than the host and other containers.

A network namespace consists of:
- IP addresses
- Network interfaces
- Routing tables
- Firewall rules / iptables
- Sockets and ports

This enables for example:
- Assigning a different public IP address to each container
- Processes in different containers uses the same port (not possible on the same host. Each process in a network namespace needs to use a different port.)

#DevOps #DataEngineering 