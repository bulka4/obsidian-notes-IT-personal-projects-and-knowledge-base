Tags: [[__Machine_Learning]]

# Introduction
Masking is a technique which can be used in an attention layer ([[Neural Network - Attention layer|link]]). 

Let's remind, that attention layer converts a set of $T$ input tokens $[x_1, \ldots, x_T]$ into a new set of $T$ output tokens $[y_1, \ldots, y_T]$, and each input token $x_i$ has an impact on how output tokens $y_j$ for other input tokens $x_j$ will look like.

Or we can say, that:
- When generating the output token $y_j$ for the input token $x_j$, we take into consideration all the other input tokens $x_i$ 
- Input token $x_j$ pays attention to other input tokens $x_i$.
# How it works
We create a mask matrix:
$$
M_{ij} \in \mathbb{R}^{T \times T}
$$
such that:
- If token $i$ is allowed to pay attention to token $j$ (i.e. $x_j$ will have an impact on $y_i$):
$$
M_{ij} = 0
$$
- If token $i$ is should not pay attention to token $j$:
$$
M_{ij} = -\infty
$$

Then we apply it when calculating weights $A = (\alpha_{ij})_{T \times T}$:
$$
A = \text{softmax}(\frac{Q K^T}{\sqrt{d_h}} + M)
$$

where:
- $\text{softmax}(-\infty) = 0$ 
- $\text{softmax}(0) = 1$ 

So using masking changes some of the weights into 0 and 1.
# Common types of masking
## Padding masking
When sequences have different length, we use PAD tokens which fills in empty fields.

For example, if we have an input like this: [token1, token2, token3, PAD, PAD]

Then mask will look like this:
$$
M = \begin{pmatrix}
0 & 0 & 0 & -\infty & -\infty \\
0 & 0 & 0 & -\infty & -\infty \\
0 & 0 & 0 & -\infty & -\infty \\
0 & 0 & 0 & -\infty & -\infty \\
0 & 0 & 0 & -\infty & -\infty \\
\end{pmatrix}
$$
That will cause, that:
- PAD tokens don't pay attention to other tokens 
- Other tokens pay attention to the PAD tokens
## Causal mask
This mask causes that future tokens don't have an impact on the past tokens, i.e. token $\large x_{t+1}$ will not have an impact on the output token $\large y_t$ , which is transformed input token $\large x_t$ .

This mask is defined as:
$$
M_{ij} = \begin{cases}
0 & j \le i \\
-\infty & j > i
\end{cases}
$$
and it looks like that:
$$
M = \begin{pmatrix}
0 & -\infty & -\infty & -\infty & -\infty \\
0 & 0 & -\infty & -\infty & -\infty \\
0 & 0 & 0 & -\infty & -\infty \\
0 & 0 & 0 & 0 & -\infty \\
0 & 0 & 0 & 0 & 0 \\
\end{pmatrix}
$$

#MachineLearning 