Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
Asynchronous request processing is an architecture where:
- Client submits a request to one service (API Gateway).
- Service immediately responds whether it received the request successfully, something like `202 Accepted`.
- Client doesn't get a result immediately and it can continue with other work
- API Gateway sends a request to another service (worker) which does the hard work in the background.
- Client received the result later using one of many different methods
# Benefits and drawbacks
[[Backend Engineering - Asynchronous request processing - Benefits and drawbacks]].
# Message queue
In asynchronous request processing ([[Backend Engineering - Asynchronous request processing|link]]), a message queue is used to store HTTP requests from an API gateway for later processing.

API gateway converts incoming HTTP requests into a job entry which is then stored in a message queue.

More information about it can be found here - [[Backend Engineering - Asynchronous request processing - Message queue]].
# Sending back a response
To send back the result to the client, there are a few patterns:
- **Pooling** ([[Backend Engineering - Asynchronous request processing - Sending back a response using pooling|link]]) - After a client (API gateway) sends a request to the worker, it checks the status later whether the task has been finished and the result is ready.
- **Webhook** ([[Backend Engineering - Asynchronous request processing - Sending back a response using webhook (callback)|link]])
	- Client (API gateway) sends request with callback URL:
	  ```json
		{
		  "jobId": "123",
		  "callbackUrl": "https://client.app/result"
		}
	  ```
	- Worker processes a job
	- When finished, worker calls the client automatically using the provided callback URL:
	  ```
		POST https://client.app/result
	  ```
- **WebSockets** ([[Backend Engineering - Asynchronous request processing - Sending back a response using WebSockets|link]])
	- Client sends a request to a worker over a connection
	- Client keeps that connection open
	- Worker pushes result when ready using the same connection
- **Shared storage** ([[Backend Engineering - Asynchronous request processing - Sending back a response via shared storage|link]])
	- Client sends a request to the worker to process
	- Worker processes it and saves results in a shared storage
	- Client can read the result whenever they want
# Event-driven architecture
Event-driven systems are systems where services send messages about events to each other:
- requester (a service) publishes an event
- Message broker receives and stores a message with information about the event
- Multiple other services receives and processes the message
- The result of processing the message is not sent back to the requester immediately, only a confirmation about receiving the message.

More information about it can be found here - [[Software Engineering - Event-driven architecture (EDA)]].
# Related topics
1. [[Backend Engineering - Asynchronous request processing - Benefits and drawbacks]]
2. [[Backend Engineering - Asynchronous request processing - Message queue]]
3. [[Software Engineering - Event-driven architecture (EDA)]]
4. [[Backend Engineering - Asynchronous request processing - Sending back a response]]
	1. [[Backend Engineering - Asynchronous request processing - Sending back a response using pooling]]
	2. [[Backend Engineering - Asynchronous request processing - Sending back a response using webhook (callback)]]
	3. [[Backend Engineering - Asynchronous request processing - Sending back a response using WebSockets]]
	4. [[Backend Engineering - Asynchronous request processing - Sending back a response via shared storage]]