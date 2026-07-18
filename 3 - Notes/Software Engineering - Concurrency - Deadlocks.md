Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A **deadlock** occurs when two or more concurrent operations are waiting for each other to release resources, so none of them can continue.

Example:
```
Thread A:
  Holds Lock 1
  Waits for Lock 2

Thread B:
  Holds Lock 2
  Waits for Lock 1
```

Result:
```
Thread A → waiting forever
Thread B → waiting forever
```
