Tags: [[_Networking]]
#Networking 

# Introduction
We can think of a network in two aspects:
- Physical network
	- A real, hardware-based connection — cables, routers, switches, etc.
	- Example: Your home Wi-Fi connects your laptop, phone, and printer.  
That’s a physical local network.
- Logical network
	- A virtual _or_ software-defined grouping of devices, regardless of physical location.

Generally in order to create a network we need to perform those high level tasks:
- Define IP address space
	- That is a list of all the available IP addresses which will be assigned to servers in this network
- Design subnets
	- Optionally we can split network into multiple separate subnets (groups).
	- Each subnet contains a group of servers from the entire network.
	- Set up a router or a gateway
	- It enables communication between subnets and to the internet (other networks).
	- Often provides NAT and firewall functions.
- Configure DNS
	- DNS will be translating names (hostnames, domain names) to IP addresses so users can connect to other servers using those names instead of IP addresses.
- Set up DHCP (Dynamic Host Configuration Protocol)
	- Automatically assigns IPs and DNS/gateway info to devices joining the network.
- Establish security controls (firewall, ACLs)
	- Control which devices and ports can communicate (e.g., block external access to internal databases).
- (Optional but common) Add directory or identity service
	- e.g., Active Directory (AD), LDAP, or Kerberos — for centralized user authentication and resource access control.

Here are some more specific examples of how we can create a network:
- Home / Office LAN
	- Router assigns IPs via DHCP and connects devices via Ethernet or Wi-Fi.
- Cloud (Azure, AWS, GCP)
	- You define a virtual network (VNet/VPC) with a CIDR range.
- Kubernetes
	- CNI plugin (e.g., Calico, Flannel) creates an internal overlay network for pods.
- Corporate network (AD Domain)
	- Admin creates an internal DNS and DHCP structure, e.g. corp.local.
