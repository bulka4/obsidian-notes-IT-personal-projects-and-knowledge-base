Tags: [[__DevOps]], [[__Infrastructure_Engineering]], [[__Cloud]] [[_Networking]]
#DevOps #InfrastructureEngineering #Cloud #Networking 

# Introduction
Connecting Azure resources to an external private network might be needed for example when:
- We run a script on Azure servers (VMs, Kubernetes, using Azure Functions etc.)
- That script needs to access a database which is outside of Azure, in another network

In order to do this, we can:
- Create an Azure VNet
- Add our Azure resource to that VNet
- Connect the VNet to an external private network
# Connecting a VNet to an external private network
To connect the VNet to an external private network, we can use:
- Site-to-Site VPN
- Private circuit (ExpressRoute-style)
## Site-to-Site VPN
- Encrypted tunnel over the public internet
- Connects:
    - Azure VNet ⟷ Company network
- Pros:
    - Cheap
    - Quick to set up
- Cons:
    - Lower bandwidth
    - Depends on internet quality

Good for:
- Dev / test
- Small to medium workloads
## Private circuit (ExpressRoute-style)
- Dedicated private connection (not internet-based)
- Very stable and fast
- Much more expensive

Good for:
- Production systems
- Strict security or compliance
- High throughput
# Other notes
- We need to create a gateway to connect an Azure VNet to another network.
- We need routing
# Questions
- Is the routing not handled within a single network?