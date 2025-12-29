Tags: [[_Computer_hardware]]

# Introduction
A GPU has a few memory levels. Each level has different size and computations using data on different levels has different speed:
- Registers - Very fast, very small
- Shared memory - Fast, small
- L2 cache - medium
- Global memory (HBM, VRAM) - Slow, very large

Calculations happen mainly in the registers and sometimes in the shared memory levels, while L2 and global memory are mainly for storage.

So usually data is transferred from the global memory and L2 into the shared memory and registers for calculations.

#ComputerHardware 