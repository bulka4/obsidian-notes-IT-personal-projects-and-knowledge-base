Tags: [[_DeepSpeed]], [[__Machine_Learning_Engineering]]

# Introduction
Rolling KV caching is an optimized version of the standard KV caching ([[DeepSpeed - KV caching|link]]).

When transformer model ([[Transformer model|link]]) generates tokens, in the standard KV caching, we keep saved K and V vectors for all the tokens generated so far. When generating a very long sequence of tokens, keeping saved all the K and V vectors, for all the tokens generated so far might be too expensive.

Rolling KV caching helps with that problem by keeping saved in cache K and V vectors only for a specific number (called window size) of past tokens. 
# How it works
When we have already saved max number of K, V vectors and we need to save them for a new token, we remove vectors for the oldest token.

When window size is n, then:
- When generating first n tokens $\large t_1, \dots, t_n$ , we save K, V vectors for all of them in cache
- When generating the token (n + k) $\large t_{n+k}$ , then:
	- We use for that K, V vectors saved in cache for the last n tokens $\large t_{k-1}, \dots, t_{n+k-1}$ 
	- After generating the token $\large t_{n+k}$ , we keep saved in cache vectors K and V for this token and we delete vectors for the oldest token $\large t_{k-1}$ 

#DeepSpeed #MLEngineering 