Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Programs request memory from the OS:
```
malloc(1000);
```

The OS/runtime allocates space in the process's address space.

When memory is no longer needed:
- manually freed (C/C++)
- garbage collected (Java, Python)