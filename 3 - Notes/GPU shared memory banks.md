Tags: [[_Computer_hardware]]

# Introduction
A shared memory ([[GPU memory levels|link]]) is an SM ([[GPU SMs (Streaming Multiprocessors)|link]]) is divided into banks. Each bank can service one memory access per cycle ([[GPU clock cycles|link]]) (during one cycle only one thread ([[GPU kernel and threads|link]]) can read data from one bank).
# Bank conflict
If **two or more threads** access different addresses in the same bank simultaneously:
- Only one access happens per cycle
- Other accesses are serialized
- Performance drops

#ComputerHardware 