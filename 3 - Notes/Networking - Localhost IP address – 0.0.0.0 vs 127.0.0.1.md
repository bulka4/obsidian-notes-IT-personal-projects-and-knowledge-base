Tags: [[_Networking]]
#Networking 

# Introduction
If we bind a process to the `127.0.0.1:<port_number>`, then we can talk to that process only from a local host, not from other servers. That's because that process will be listening only on a loopback interface.

We need to bind a process to the `0.0.0.0:<port-number>` in order to be able to talk to it from other servers. It will be listening then on all network interfaces.