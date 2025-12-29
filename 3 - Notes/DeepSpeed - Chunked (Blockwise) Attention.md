Tags: [[_DeepSpeed]], [[__Machine_Learning_Engineering]]

# Introduction
In a standard attention layer ([[Neural Network - Attention layer|link]]), during generating tokens ([[Token generation|link]]) using a transformer model ([[Transformer model|link]]), when generating each output token we need to:
- Calculate Q, K and V vectors 
- Use K and V vectors calculated earlier for every generated token

This becomes problematic when:
- Input sequence is long
- We use big batch sizes ([[Batching|link]])
- We use beam search ([[Token generation - Beam Search|link]]) or speculative decoding ([[Token generation - Speculative Decoding|link]])

Chunked Attention helps with this by splitting calculations in an attention layer into multiple steps. At each step we perform calculations only on a subset of all data.

We don't change the math behind an attention layer, we receive the same results. We just modify the way how calculations are performed.
# How it works
We split K and V vectors into fixed-size chunks. Each chunk contains whole K and V vectors for a subset of all input tokens.

For each chunk:
- We load K and V vectors from that chunk
- Calculate partial attention scores

Then we accumulate results from all the chunks to calculate an output needed for generating given output token. Then we do the same for generating next tokens.
## Compute partial scores
We have $\large K, V \in \mathbb{R}^{T \times d}$ metrices, where each row $\large K_{i :}, V_{i :}$ are vectors for a single input token.

We split them into smaller matrices:
$$
(K, V) = [(K_1, V_1), \ldots, (K_n, V_n)]
$$
where $\large K_c, V_c \in \mathbb{R}^{t \times d}$ are matrices for a subset of $t$ tokens. So each chunk $K_c, V_c$ contains only a subset of rows of $K, V$ which corresponds to a subset of all tokens.

and calculate partial attention scores for tokens in each chunk $c$ :
$$
\large s_{c,i} = \frac{Q K_{c,i}^T} {\sqrt{d}}
$$
Where:
- $Q$ is a vector for the currently processed input token (non-chunked)
- $\large K_{c,i}$ - The $i$-th row of $\large K_c$ , that is a vector for the $i$-th token in the chunk $c$ 
## Softmax
We will use partial attention scores $\large s_{c, i}$ from all the chunks to calculate the same value as softmax:
$$
\text{softmax}(s_i) = \frac{\exp (s_i)}{\sum_{j} \exp (s_j)}
$$
for $s_i$ scores for non-chunked matrices $K, V$ and token $i$.

We do this using the following algorithm:

We maintain:
- m - Running max
- l - Running sum of exp
- o - Running output accumulator

For each chunk i:
- Compute chunk max:
$$
\large m_c = \max(s_{c,i})
$$
- Update global max:
$$
\large m_{\text{new}} = \max(m, m_c)
$$
- Rescale old sums:
$$
\large l = l \cdot \exp(m - m_{\text{new}})
$$
- Add chunk contribution:
$$
\large l = l + \sum_{i=1}^t \exp(s_i - m_{\text{new}})
$$
- Accumulate output:
$$
\large \begin{align}
& o = o \cdot \exp(m - m_{\text{new}}) \\
& o = o + \sum_{i=1}^t \exp(s_{c,i} - m_{\text{new}}) \cdot V_{c, i}
\end{align}
$$
- Update $m = m_{\text{new}}$ 

After all chunks:
$$
\large \text{final output} = \frac{o}{l}
$$
# How it works with blockwise KV cache
Blockwise Attentions works nicely with the blockwise KV cache ([[DeepSpeed - Blockwise KV Storage (Paged KV-cache)|link]]). We calculate partial attention scores using K and V vectors from one KV cache block (corresponding to a subset of input tokens).
# Benefits
GPU memory consists of different levels as described here - [[GPU memory levels|link]]. If we load all the K and V vectors from the cache, they might not fit in the memory level where calculations are fastest (registers level) and part of this data will be saved in other memory levels.

In that case, K and V vectors saved in other levels will need to be transferred into the registers level to enable fast calculations and some of them might be transferred multiple times.

#DeepSpeed #MLEngineering 