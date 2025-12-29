Tags: [[_DeepSpeed]], [[__Machine_Learning_Engineering]]

# Introduction
As explained here - [[DeepSpeed - KV caching|link]], DeepSpeed can cache values of K and V vectors (Key and Value) used in a transformer model when generating tokens.

Instead of storing KV-cache as one long tensor, DeepSpeed can store it in fixed-size memory blocks (“pages”).
# How blockwise storage helps
Each sequence gets a list of blocks:

`Block 0 → Block 1 → Block 2 → ...`

Each block stores K/V for maybe **16 or 32 tokens**.

Benefits:
- Avoiding duplicating data
	- For example in beam search ([[Token generation - Beam Search|link]]), the same tokens in different beams use the same blocks instead of creating copies of KV vectors for the same tokens in different beams
- Easier modification of a sequence of tokens
	- Sometimes we need to add a new token or replace the existing one with a new one, like in speculative decoding ([[Token generation - Speculative Decoding|link]])
	- It is easier to add a new block or replace a single block than modifying one big KV tensor which holds vectors for all tokens
- Better GPU utilization
	- We can load only the blocks that are needed instead of the entire tensor
- Helps avoiding memory fragmentation and reallocation - [[Memory fragmentation and reallocation|link]]
	- Within a block, KV vectors are stored contiguously (close to each other) in memory
	- Blocks are reusable, thanks to which we avoid copying data (less data = less problems with fragmentation and reallocation)
- Reordering of data is easier
	- For example in beam search, we need to reorder beams (order them according to their score), after that we need to map which KV vectors in memory correspond to which, reordered beams.
		- Without blockwise storage, we need to modify the entire KV tensor to match the new order
		- With blockwise storage, we just change pointers which indicate, which blocks each beam reference

#DeepSpeed #MLEngineering 