Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Disks store data in fixed-size blocks which are groups of bytes.

Example:
```
File:
"Hello world"

Filesystem:

Block 100 → "Hello"
Block 101 → " world"
```

The filesystem keeps track of which blocks belong to which files.