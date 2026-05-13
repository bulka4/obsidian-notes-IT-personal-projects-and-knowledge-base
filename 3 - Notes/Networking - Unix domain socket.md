Tags: [[_Networking]]
#Networking 

# Introduction
A Unix Domain Socket (UDS) is a communication endpoint used for inter-process communication (IPC), that is a communication between processes running on the same host machine.

Unlike network sockets, which use IP addresses and port numbers for addressing, Unix domain sockets use file system paths as their addresses.

A Unix domain socket appears as a special file in the filesystem, which represents the communication endpoint. The file path uniquely identifies this endpoint and is used by processes to establish communication.

Because Unix domain sockets bypass the network stack, they offer faster communication compared to network sockets.