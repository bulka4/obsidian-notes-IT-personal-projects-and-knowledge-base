Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Backpressure is a mechanism that prevents a fast producer from overwhelming a slower consumer.

If one component cannot process data fast enough, it tells the sender to slow down or stop sending temporarily.

For example. when producer generates 1000 messages/second and consumer can process only 100 messages/second, then messages pile up in memory, queues grow, and eventually the system may run out of memory or become very slow.

With backpressure, the consumer signals that it is overloaded, so the producer reduces its sending rate.