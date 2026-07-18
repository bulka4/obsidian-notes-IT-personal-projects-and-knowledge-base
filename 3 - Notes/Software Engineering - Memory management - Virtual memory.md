Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Each process gets its own virtual address space, i.e. another address space ([[Memory addresses|link]]) different then the real address space, so:
- The same address in the virtual space and in the real space can point to different physical memory locations
- There is a mapping between addresses in both spaces, e.g. address `0x0000` in the virtual space corresponds to the `0x0001` address in the real space (so they point to the same physical memory location)

Different programs can have the same address space (virtual):
```
Process A:
0x0000 ──────────
        code
        data
        heap
        stack
0xFFFF ──────────

Process B:
0x0000 ──────────
        code
        data
        heap
        stack
0xFFFF ──────────
```

But the OS maps these virtual addresses to actual physical memory locations:
```
Virtual addresses

Process A:
0x1000  ───────→ Physical RAM address 5000

Process B:
0x1000  ───────→ Physical RAM address 9000
```

This provides:
1. **Isolation**
    - A program cannot directly access another program's memory.
2. **Simpler programming**
    - Programs see a continuous memory space even if physical RAM is fragmented.
3. **Memory efficiency**
    - The OS can move pages between RAM and disk (swap).
4. **More memory than RAM**
    - A process can have a larger virtual address space than available physical memory.