Tags: [[_Computer_hardware]] [[__Infrastructure_Engineering]] [[_Software_Engineering]]
#ComputerHardware #InfrastructureEngineering #SoftwareEngineering 

# Introduction
SIMD (Single Instruction, Multiple Data) is a CPU feature that allows one instruction to operate on multiple pieces of data at the same time.

Without SIMD:
```
Instruction: add
Data:
1 + 5 = 6

Instruction: add
Data:
2 + 6 = 8

Instruction: add
Data:
3 + 7 = 10
```

The CPU performs each operation separately.

With SIMD:
```
One instruction:

[1, 2, 3, 4]
+
[5, 6, 7, 8]

=

[6, 8, 10, 12]
```

One CPU instruction processes multiple values at once.
# How it works
Modern CPUs have special registers:
```
Normal register:

[ 64-bit value ]

SIMD register:

[ value ][ value ][ value ][ value ]
```

A SIMD instruction applies the same operation to all elements.

Examples:
- add multiple numbers
- multiply vectors
- compare multiple values
# Common SIMD instruction sets
- **SSE** (older Intel/AMD)
- **AVX / AVX2 / AVX-512** (newer Intel/AMD)

Example:
```
AVX register:

[float][float][float][float][float][float][float][float]
```
One instruction can operate on many floats.
# Why it matters
SIMD is useful for workloads with lots of identical operations:
- image processing
- video encoding
- numerical computing
- machine learning
- scientific computing