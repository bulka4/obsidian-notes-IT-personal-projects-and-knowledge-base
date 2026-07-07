Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Webhook (callback) is one of methods of sending back a response in asynchronous request processing ([[Backend Engineering - Asynchronous request processing - Sending back a response|link]]).

It works like this:
- Client sends request with callback URL:
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