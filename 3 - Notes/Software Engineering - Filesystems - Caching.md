Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Reading from disk is slow, so the OS keeps frequently used data in RAM:
```
Application
    |
    ↓
Filesystem cache
    |
    ↓
Disk
```

Example:

First read:
```
Disk → RAM → Application
```

Second read:
```
RAM → Application
```

Much faster.