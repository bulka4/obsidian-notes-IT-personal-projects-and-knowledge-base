Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Scalability testing is a type of performance testing that checks how well a system handles increasing workload by adding resources.

The question:
> "Can the system grow as demand increases?"
# Example
You have an API:
```
1 server:
  5,000 requests/sec

2 servers:
  9,800 requests/sec

10 servers:
  45,000 requests/sec
```

You check whether adding more servers actually improves capacity.