Tags: [[_Networking]]
#Networking 

# Introduction
Each Ipv4 address, like 192.168.1.0 is a 32 bit number.

It consists of 4 numbers separated by dots, in that case 192, 168, 1 and 0, and each number is represented as 8 bits.
## CIDR

CIDR is a way specifying an IP address range.

It uses CIDR blocks which looks like this:

· IP_address/x

Where x is a number between 0 and 32.

For example a CIDR block might look like this:

· 192.168.1.0/24

That example CIDR block indicates that:

· IP address range starts at 192.168.1.0

· /24 means that the first 24 bits out of 32 are fixed, so the remaining 8 bits are variable

· That means that this range includes 2^8 = 256 IP addresses: from192.168.1.0 to 192.168.1.255

In order to understand what those bits means please refer to the previous section ‘IP address bits’.