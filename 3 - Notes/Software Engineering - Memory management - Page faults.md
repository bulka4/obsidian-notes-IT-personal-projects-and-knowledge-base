Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
If a program accesses memory that is not currently in RAM:
1. CPU asks for a page ([[Software Engineering - Memory management - Pages and paging|link]])
2. OS detects it is missing
3. OS loads it from disk (swap or file)
4. Program continues

This is called a page fault.

Disk access is much slower than RAM, so many page faults hurt performance.