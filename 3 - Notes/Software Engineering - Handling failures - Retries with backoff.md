Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Retries with backoff is a technique of sending another request after one request failed. Before sending every next request, we wait some time. After every request, we wait longer then previously, for example:
```
attempt 1 -> 
wait 1s -> attempt 2 -> 
wait 2s -> attempt 3 -> 
wait 4s -> attempt 4 ->
wait 8s -> ...
```
