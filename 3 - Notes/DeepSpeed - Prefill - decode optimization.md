Tags: [[_DeepSpeed]], [[__Machine_Learning_Engineering]]

# Introduction
When using a transformer model ([[Transformer model|link]]) for token generation ([[Token generation|link]]), it is good to split the process into two parts because they have different challenges:
- Prefill - Processing the input sequence of tokens
	- We perform a lot of computations in parallel
- Decode - Generate output tokens
	- We generate tokens one by one
	- There is little calculations but we often read and save data from/in memory (K, V vectors from cache ([[DeepSpeed - KV caching|link]]))
# Prefill
Prefill is compute-bound, that means that the main problem is a big amount of calculations to perform.

The most costly operations are large matrix multiplications in the attention ([[Neural Network - Attention layer|link]]) and dense layers ([[Neural Network - Fully-connected (dense) layer|link]]) (including calculating Query, Key and Value (Q, K, V) vectors).

Then we save calculated K and V vectors in memory using KV caching ([[DeepSpeed - KV caching|link]]) so they can be used during decoding (generating output tokens).
# Decode
Decode is memory-bound and latency-bound, that means that the main problem is big amount of data we need to store in memory and latency.

During decode, we don't perform so many computations in parallel like in case of a prefill. The main challenges are:
- Memory
	- Keeping all the K, V vectors in a cache
- Latency
	- Memory latency - It takes time to read and save K, V vectors from/in a cache. For every new generated token, we calculate new K and V vectors and save them in cache
	- Kernel launch latency ([[GPU kernel and threads|link]]) - It takes time to launch calculations on GPU

There is little calculations to do in parallel because we perform calculations only for one token at a time.

But we start new calculations often, for every new token we start new calculations and that require reading and saving data from/in memory and launching GPU kernels which takes time.

Optimizations like kernel fusion ([[DeepSpeed - Kernel fusion|link]]), blockwise KV storage ([[DeepSpeed - Blockwise KV Storage (Paged KV-cache)|link]]), chunked attention ([[DeepSpeed - Chunked (Blockwise) Attention|link]]) , sliding window attention, and MQA/GQA ([[DeepSpeed - MQA and GQA|link]]) mainly target the decode phase, because that phase is dominated by memory access and launch overhead.
# Techniques used for prefill and decode
## Batching
Thanks to batching ([[Batching|link]]), total time for processing all requests is smaller (throughput is higher) because GPUs are more efficient when executing more calculations in parallel rather than one by one. 

But batching can cause bigger latency (delay) for some of the input sequences. That's because all input sequences are processed together so we receive results (output tokens) for them at the same time.

So when our batch contains:
- Small sequences which can be processed quickly
- Big sequences which require more time to process
Then we still receive results for all sequences in the batch at the same time, so smaller sequences need to wait for bigger ones.

If we process small sequences separately, we would receive results for them faster.

Usually it is beneficial to use batching during prefill to quickly prepare K and V vectors needed for generating output tokens for many input sequences. That will cause that some users will need to wait longer for start of generating response but all responses in total will be generated faster.

Usually we use smaller batches during decode because then we generate tokens one by one so for every input sequence in the batch, we generate each token at the same time. Bigger batches can cause bigger delays between generating next tokens for some sequences (which are faster to process on their own).

So usually we use bigger batches during prefill and smaller during decode because usually waiting longer for token generation to start is better than bigger delays between generating different tokens for the same input sequence after generation starts.

#DeepSpeed #MLEngineering 