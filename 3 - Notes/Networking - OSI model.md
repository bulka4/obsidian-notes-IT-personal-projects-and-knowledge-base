Tags: [[_Networking]]
#Networking 

# Introduction
It is a conceptual framework used to understand how network systems communicate in layers.

It has the following layers:

1. Physical

1.1. The actual hardware (cables, switches, electrical signals)

2. Data Link

2.1. Transfers frames between devices on the same network (e.g., Ethernet, MAC addresses)

3. Network

3.1. Routing data across networks (e.g., IP addresses)

4. Transport

4.1. Reliable delivery (e.g., TCP/UDP)

5. Session

5.1. Manages sessions between applications

6. Presentation

6.1. Translates data (e.g., encryption, compression)

7. Application

7.1. Interfaces with apps (e.g., browsers, APIs)

## Data Link Layer

It defines how devices on the same physical or virtual network (like LAN) talk to each other.

It uses MAC addresses to identify devices.

It packages data into frames to be sent over the network.

Examples of Data Link Layer protocols:

· Ethernet

· Wi-Fi

## Network Layer

It handles routing and forwarding of data packets between devices across different networks.

Key functions of this layer:

· Addressing

o It uses IP addresses to identify source and destination devices on the network.

· Routing

o Determines the best path for data to travel from source to destination

· Packet Forwarding

o Transfers packets from one network segment to another using routers

Common protocols in this layer:

· IP (IPv4, IPv6 – for IP addresses)

## Transport layer

Key functions:

· **Segmentation and reassemly**

o Breaks big packets of data into smaller pieces at a sender and reassemblies them at a receiver.

· **Connection Management**

o **Connection-oriented communication** (e.g., TCP): Establishes, maintains, and terminates a connection.

o **Connectionless communication** (e.g., UDP): No session is maintained between devices

Popular protocols in this layer:

· TCP

· UDP

## Session Layer

It is responsible for creating, managing and terminating sessions between applications.

When two applications / devices want to talk to each other, a session is created and used for exchanging information. When the conversation ends the session is done.