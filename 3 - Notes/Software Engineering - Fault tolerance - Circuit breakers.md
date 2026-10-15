Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
A circuit breaker is a protection mechanism for handling unreliable external dependencies (e.g. when making API calls to an external system).

When requests continue failing for a long time, then for some time, every time we want to make a request, we perform some other, alternative action instead.
# States
A circuit breaker has 3 states:
### Closed (normal)
- Requests go through (to one or multiple external services)
- If failures happen:
	- they’re tracked (we count how many failures appears in total for all services)
	- we can use retries, do anything we want with the received errors
- If a number of failures exceeds a threshold, we go to the open state
### Open (fail fast)
- No more sending requests to the failing, external system
- Every time we want to make a request to the external system, we perform an alternative action instead:
	- Return fallback (e.g. cached data)
	- Skip the step / mark as retry later
	- Or fail fast (if no fallback exists)

Prevents:
- Wasting resources
- Cascading failures
### Half-open (test)
- Allow a few requests
- If they succeed → back to normal (closed)
- If they fail → open again
### State change flow
States changes like that:
- Start with a closed state
- If a number of failures exceeds a threshold, go to open state
- Stay in an open state for a specified amount of time
- Go to a half-open state after that time