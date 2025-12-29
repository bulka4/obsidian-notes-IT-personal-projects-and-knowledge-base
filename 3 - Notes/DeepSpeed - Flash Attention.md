Tags: [[_DeepSpeed]], [[__Machine_Learning_Engineering]]

# Introduction
Flash attention is blockwise attention ([[DeepSpeed - Chunked (Blockwise) Attention|link]]) which is optimized to run on GPUs. It uses:
- kernel fusion
- register-level blocking
- shared-memory tiling
- minimized memory traffic
- warp-level synchronization
- numerical softmax tricks tuned for GPUs

So math is the same as in the blockwise attention but execution on GPUs differs.
# Kernel fusion
Normally, we use separate GPU kernels ([[GPU kernel and threads|link]]) to calculate:
- Scores $QK^T$
- Applies score scaling and softmax
- Multiplies scores by the $V$ vectors

Flash attention fuse those kernels into a single kernel ([[DeepSpeed - Kernel fusion|link]]).
# Register level design
Flash attention stores less data outside of the register level memory of GPU ([[GPU memory levels|link]]) on which it performs calculations which is faster.
# Blocks aligned with GPU warps and SMs
Flash Attention chooses block sizes that:
- Exactly match warp ([[GPU Warps|link]]) sizes (one warp has enough threads to perform calculations on data from the entire block)
- Maximize occupancy (number of active warps per SM ([[GPU SMs (Streaming Multiprocessors)|link]]))
- Avoid bank conflicts in shared memory ([[GPU shared memory banks|link]])
	- It is done by saving data in shared memory in such a way, that different threads access data in different banks

It also uses other tricks which gives additional benefits:
- No warp divergence ([[GPU Warps|link]]) in softmax loops
- Memory is coalesced
	- Data is stored in memory in such a way that its bytes has assigned neighboring addresses ([[Memory addresses|link]]), thanks to which it can be read faster.
# One-pass numerically stable softmax (GPU-tuned)
Flash Attention:
- Calculates softmax using chunks inside the fused kernel
- Avoids:
    - extra passes over data
    - reloading chunks
- Uses:
    - fast `exp2` instead of `exp` (that is $2^x$ instead of $e^x$)
    - scaling tricks to avoid overflow (that is to avoid a situation when $e^x$ is too big to be represented using formats such as FP16, FP32 ([[Numeric formats (precision)|link]]))
    - reduced precision where safe (FP16/BF16)

This makes it:
- Stable
- Exact
- Faster than a naïve online softmax
# Backward pass is also fused and memory-optimal
Flash Attention also:
- Fuses backward pass kernels (i.e. fuses kernels during calculating backpropagation ([[Backpropagation|link]]))
- Recomputes parts of attention on the fly instead of storing intermediates
- Minimizes activation storage (storage of outputs of activation functions)

This dramatically reduces training memory vs “chunked forward + standard backward”.
# Hardware-aware precision handling
Flash Attention:
- Uses mixed precision ([[Numeric formats (precision)|link]]) carefully
- Accumulates in FP32 when needed
- Uses Tensor Cores ([[NVIDIA GPU Tensor Cores|link]]) optimally

#DeepSpeed #MLEngineering 