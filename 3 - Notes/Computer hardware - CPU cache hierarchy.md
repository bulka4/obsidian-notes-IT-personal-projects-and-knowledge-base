Tags: [[_Computer_hardware]] [[__Infrastructure_Engineering]] [[_Software_Engineering]]
#ComputerHardware #InfrastructureEngineering #SoftwareEngineering 

# Introduction
CPU cache hierarchy is a system of small, very fast memory areas close to the CPU that store frequently used data and instructions.

The goal:
> Keep frequently needed data close to the CPU to avoid slow access to RAM.

Hierarchy of stores from the fastest to the slowest when it comes to reading data from it:
- CPU Registers
- L1 cache
- L2 cache
- L3 cache
- RAM
- Disk
# Cache hit / miss
- **Cache hit** means that data found quickly in a cache
- **Cache miss** means that CPU waits for slower memory