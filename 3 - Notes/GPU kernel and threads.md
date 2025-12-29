Tags: [[_Computer_hardware]]

# Introduction
GPU kernel is a function (code) which defines what calculations to perform on a GPU.

Threads are processes running on a GPU which execute kernel's code on different subsets of data in parallel. We can specify in kernel's code, how many threads we want to create and which parts of data each of them will be processing.

For example, let's assume that we want to add vectors:
$$
[1,2] + [1,2] = [2,4]
$$
and we have the following kernel for adding vectors:
```
__global__ void add_vectors(float* a, float* b, float* out) {
    int idx = threadIdx.x;   // Each thread gets a different index
    out[idx] = a[idx] + b[idx];
}
```

In this kernel, we specify that each thread will be responsible for performing calculations on separate elements of vectors.

So in this example:
- One thread will add first elements of vectors a[0] + b[0] = c[0] (1+1 = 2)
- Second thread will add second elements of vectors a[1] + b[1] = c[1] (2 + 2 = 4)

#ComputerHardware 