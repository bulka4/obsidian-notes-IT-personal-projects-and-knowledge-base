Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
A deadlock occurs when two or more concurrent operations are waiting for each other to release resources (locks), so none of them can continue. This can refer to operations within a single application or to multiple applications.

Example:
```
Thread A:
  Holds Lock 1
  Waits for Lock 2

Thread B:
  Holds Lock 2
  Waits for Lock 1
```

So the Thread A waits for the Lock 2 while performing operation for which it acquired the Lock 1. Similarly for the Thread B

As a result, both threads wait forever.