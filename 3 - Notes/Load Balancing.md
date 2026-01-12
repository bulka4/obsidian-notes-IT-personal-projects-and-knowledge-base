Tags: [[__Web_Development]]
#WebDevelopment 

# Introduction
Load balancing is a practice of distributing incoming network traffic (requests) across multiple servers to ensure no single server gets overwhelmed.
# Benefits
- Better performance
	- Faster responses, since a single server has less requests to handle
- Increased reliability
	- When one server fails, others can still handle requests
- Horizontal scaling
	- When traffic grows and our servers are starting having problems to handle all of them, we can add more servers to increase total computational power
# Load balancing strategies
We can perform load balancing in different ways:
- Round-robin
	- Each request goes to the next server in line
- Least connections ([[Web app connections|link]])
	- New request goes to the server which has the least active connections
- Weighted distribution
	- More powerful servers get more requests
- Distribution based on request size and computational resources
	- Consider how much computational power each request requires and how much computational power each server has available