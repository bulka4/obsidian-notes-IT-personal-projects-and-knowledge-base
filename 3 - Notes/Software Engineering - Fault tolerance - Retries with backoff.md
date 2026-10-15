Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
Retries with backoff is a technique where we:
- when a request fails, send another one after some time
- after every request, we wait longer then previously

For example:
```
attempt 1 -> 
wait 1s -> attempt 2 -> 
wait 2s -> attempt 3 -> 
wait 4s -> attempt 4 ->
wait 8s -> ...
```
