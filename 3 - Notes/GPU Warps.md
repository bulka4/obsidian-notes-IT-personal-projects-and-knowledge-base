Tags: [[_Computer_hardware]]

# Introduction
A GPU warp is the smallest execution unit on an NVIDIA GPU:
- 1 warp = 32 threads ([[GPU kernel and threads|link]])
- All 32 threads execute the same instruction on different data
- This is called SIMT (Single Instruction, Multiple Threads)
# Warp divergence
Warp divergence is a situation when threads in the same warp need to perform different calculations.

For example, let's assume we have a code which adds vector elements if that sum is bigger than 0 and if it's smaller, then subtract them:
```
__global__ void add_or_sub_vectors(float* a, float* b, float* out) {
    int idx = threadIdx.x;   // Each thread gets a different index
    float sum = a[idx] + b[idx];

    // Divergent branch
    if (sum > 0.0f) {
        out[idx] = a[idx] + b[idx];   // path A
    } else {
        out[idx] = a[idx] - b[idx];   // path B
    }
}
```

This is a similar example to the one explained in this document - [[GPU kernel and threads|link]], we just have additionally an 'if' statement which creates two different paths - different codes to execute depending on whether the given condition true. 

As explained in that document, performing calculations for each element of input vectors is performed by different threads.

If we only add vector elements in this example, then each thread would perform the same operation (adding). But since we have an 'if' statement, we have different operations for different elements of those vectors - adding and subtracting. 

So some threads will be performing adding while others will be subtracting, depending on what are the vectors values assigned to each thread.
## Masking threads
GPU doesn't perform both paths A and B (adding and subtracting) in parallel but sequentially, one by one.

At each step, a part of threads is masked (disabled). That means, that only a part of threads is performing calculations for one path. First, one part of threads performs adding, then the other part is subtracting.
## Performance
Divergence can lower performance, since we perform calculations sequentially instead of in parallel.

#ComputerHardware 