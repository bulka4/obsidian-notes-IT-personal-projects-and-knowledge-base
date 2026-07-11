Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Scaling means increasing a system's ability to handle more workload, usually by increasing:
- the number of requests it can process,
- the amount of data it can handle,
- the number of users it can serve.

There are two main approaches:
1. Vertical scaling (scale up) - 
2. Horizontal scaling (scale out) - 
# Vertical scaling
Increase the resources of a single machine (CPU, RAM etc.).

Benefits:
- It is simple - no need to manage multiple instances of a service.

Drawbacks:
- Hardware limits - we can't infinitely increase CPU/RAM
- Single point of failure - If the server fails, the whole application may go down.
- Expensive - Very powerful machines become disproportionately expensive
# Horizontal scaling
Add more instances of the application. There are two variations:
- Create additional replicas of the service on the same server
- Add more servers and create additional replicas of the service on them
## Create additional replicas of the service on the same server
Benefits:
- Better CPU utilization - Multiple processes can use multiple CPU cores
- Better concurrency - If one instance is busy, others can handle requests
- Isolation - If one instance crashes, others can handle requests

Drawbacks:
- All instances share the same hardware which may become too weak at some points
## Add more servers and create additional replicas of the service on them
Benefits:
- Much higher capacity
- Fault tolerance - If one server fails, others can take over
- Geographic distribution - We can place servers in different places on Earth such that all users have servers nearby. Server closer to users = lower latency.

Drawbacks:
- More complex and expensive
- Data consistency problems - Multiple servers may have different views of data, e.g:
  ```
	Server A:
	User balance = $100
	
	Server B:
	User balance = $120
  ```
