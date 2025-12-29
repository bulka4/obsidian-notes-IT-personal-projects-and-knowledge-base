Tags: [[_Computer_hardware]]

# Introduction
An SM (Streaming Multiprocessor) is a compute unit of an NVIDIA GPU.

It is like a CPU core but it runs thousands of tiny threads ([[GPU kernel and threads|link]]) in parallel. Each SM contains:
- Many CUDA cores (for math operations on numbers) ([[NVIDIA GPU Cuda Cores|link]])
- Tensor Cores (for math operations on matrices) ([[NVIDIA GPU Tensor Cores|link]])
- Registers and shared memory ([[GPU memory levels|link]])
- Schedulers for threads

Each SM is independent of other SMs.
# Running warps
Each SM runs many warps ([[GPU Warps|link]]) at the same time but not all of them. It schedules which warps should start calculations when.
## Switching warps
When some of the warps are stall because they wait to load necessary data from slower memory levels ([[GPU memory levels|link]]) like global memory, SM can start in that time other warps.

This hides memory latency. When one wrap waits for data to be loaded from memory, other wrap starts its own calculations using different data.

#ComputerHardware 