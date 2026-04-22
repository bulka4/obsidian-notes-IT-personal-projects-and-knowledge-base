Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A circuit breaker is a protection mechanism for handling unreliable external dependencies (like APIs).

It is used for example when we try to make an API call many times, regularly.

It prevents from performing too many failing actions.

It has 3 states:
### Closed (normal)
- Requests go through
- If failures happen → they’re tracked (we count how many failures appears)
- If a number of failures exceeds a threshold, we go to the open state
### Open (fail fast)
- No more calls to the failing system
- Every time we want to make a request, we perform an alternative action instead:
	- Return fallback (e.g. cached data)
	- Skip the step / mark as retry later
	- Or fail fast (if no fallback exists)

Prevents:
- Wasting resources
- Cascading failures
### Half-open (test)
- Allow a few requests
- If they succeed → back to normal
- If they fail → open again
### State change flow
States changes like that:
- Start with a closed state
- If a number of failures exceeds a threshold, go to open state
- Stay in an open state for a specified amount of time
- Go to a half-open state after that time