Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Clock synchronization is about making sure that computers in a distributed system ([[Backend Engineering - Distributed microservices|link]]) agree on what the time is.

Time on different servers might not be synchronized perfectly, so for example we could have a situation where:
- When on server A is 10:00:05, on server B it is 10:00:02
- Server A sends a message at 10:00:05 according to its time
- Server B receives that message at 10:00:03 according to its time
# How synchronization works
Usually, computers synchronize against a time source. The servers periodically ask the time server "what time is it?" and adjust their clocks.

The most common protocol is: NTP (Network Time Protocol).
# NTP (Network Time Protocol)
Using NTP, client measures:
- when it sent the request
- when it received the response

So it considers network delay when asking a time server about the time and adjusting its clock.
# Problem
Even when we measure the time between sending the request to a time server and receiving a response:
```
Client                         Time Server

  t1 -------------------------> t2
        network delay 1

  t3 <------------------------- t4
        network delay 2
```

we know only the total delay `delay 1` + `delay 2` but we don't know exactly how long is `delay 1` and `delay 2` so we still can't precisely determine what exactly is the current time.