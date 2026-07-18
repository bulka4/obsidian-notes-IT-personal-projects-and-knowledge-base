Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Load balancing is a practice of distributing incoming network traffic (requests) across multiple services to ensure no single service gets overwhelmed.
# Benefits
- Better performance
	- Faster responses, since a single service has less requests to handle
- Increased reliability
	- When one service fails, others can still handle requests
- Horizontal scaling
	- When traffic grows and our services are starting having problems to handle all of them, we can add more instances of a service or more servers to increase total computational power
# Load balancing strategies
We can perform load balancing in different ways:
- Round-robin
	- Each request goes to the next service in line
- Least connections ([[Web app connections|link]])
	- New request goes to the service which has the least active connections
- Weighted distribution
	- More powerful servers get more requests
- Distribution based on request size and computational resources
	- Consider how much computational power each request requires and how much computational power each server has available