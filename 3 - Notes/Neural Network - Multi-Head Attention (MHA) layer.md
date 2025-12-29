Tags: [[__Machine_Learning]]

# Introduction
This document describes a multi-head attention (MHA) layer for neural networks, which is an extension of a single-head version described here - [[Neural Network - Attention layer]].

To get better intuition about how it works and how to interpret it, refer to the mentioned document.

The main difference, is that in the single-head version we have one set of matrices with trainable weights:
$$
\large
W_q, W_k, W_v \in \mathbb{R}^{d \times d}
$$
And in the multi-head version, there are multiple sets:
$$
\large
W_q^{(h)}, W_k^{(h)}, W_v^{(h)} \in \mathbb{R}^{d \times d_h}, \quad h = 1, \ldots, H 
\text{ - Head number}
$$
which are used to generate separate outputs per her $\large y^{(h)} \in \mathbb{R}^{d_h}$, which are then concatenated ([[Concatenating matrices|link]]) to create the final output $\large y = (y^{(1)}, \ldots, y^{(H)})$.
# How it works - Calculations
Here we describe mathematically what calculations attention layer performs to generate the output.

We divide this section into two subsections:
- Calculating a single output token - How to calculate a single output token $y_i$ 
- Calculations with a matrix notation - How to calculate all the output tokens $Y = [y_1, \ldots, y_T]$ using matrix variables
## Calculating a single output token
This section describes how to calculate a single output token $y_i$ .

Input is the same as in case of a single-head version:
$$
\large
X = [x_1, \ldots, x_T] \in \mathbb{R}^{T \times d}, \quad x_i \in \mathbb{R}^d
$$
which is a set of vectors (tokens), that is a 2-D tensor (matrix) of shape $(T, d)$, where:
- $T$ - Input length (sequence length)
- $d$ - Dimension of each token in a sequence

And output is also of shape $(T, d)$:
$$
\large
Y = [y_1, \ldots, y_T] \in \mathbb{R}^{T \times d}, \quad y_i \in \mathbb{R}^d
$$

For each head $h = 1, \ldots, H$ we have separate matrices with trainable weights:
$$
\large
W_q^{(h)}, W_k^{(h)}, W_v^{(h)} \in \mathbb{R}^{d \times d_h}
$$
where:
$$
\large
d_h = \frac{d}{H}
$$
so each head outputs vectors of length $d_h$, smaller than $d$.

Now we calculate $Q, K$ and $V$ (Query, Key and Value) for each input token and for each head:
$$
\large 
Q_i^{(h)} = x_i W_q^{(h)}, \quad
K_i^{(h)} = x_i W_k^{(h)}, \quad
V_i^{(h)} = x_i W_v^{(h)}, \quad
Q_i^{(h)}, K_i^{(h)}, V_i^{(h)} \in \mathbb{R}^{d_h}

$$
Each of those values now have smaller dimension $d_h$ instead of $d$.

Now we calculate scores per head:
$$
\large
\text{score}_{ij}^{(h)} = Q_i^{(h)} K_j^{(h)T}
$$
which indicates how related are input tokens $x_i$ and $x_j$ .

Then, we scale those scores:
$$
\large 
\text{score}_{ij}^{{(h)}\text{ scaled}} = \frac{Q_i^{(h)} K_j^{(h)T}}{\sqrt{d_h}}
$$
and use a softmax function to convert them into weights with value in the range $[0, 1]$ :
$$
\large
\alpha_{ij}^{(h)} = \frac{\exp( \text{score}_{ij}^{{(h)}\text{ scaled}} )} 
{ \sum_{k=1}^T \exp( \text{score}_{ik}^{{(h)}\text{ scaled}} ) }
\in [0,1]
$$
also softmax makes sure, that $\large \sum_{j} \alpha_{ij}^{(h)} = 1$ .

The output is weighted sum of all the input tokens:
$$
\large
y_i^{(h)} = \sum_{j=1}^T \alpha_{ij}^{(h)} V_j^{(h)} \in \mathbb{R}^{d_h}
$$
So it is a mix of Values V of all the input tokens, with assigned weights indicating how relevant is the input token $j$ to the input token $i$.

Now we concatenate ([[Concatenating matrices|link]]) outputs from all the heads:
$$
\large
y_i^{\text{concat}} = (y_i^{(1)} \dots y_i^{(H)}) \in \mathbb{R}^{H \cdot d_h}
= \mathbb{R}^{d}
$$
and multiply it by another matrix with trainable weights to generate the final output token:
$$
\large
y_i = y_i^{\text{concat}} W_o, \quad W_o \in \mathbb{R}^{d \times d}
$$

Set of all the output tokens:
$$
Y = [y_1, \ldots, y_T] \in \mathbb{R}^{T \times d}
$$
matches the shape of the input $X$ .
## Calculations with a matrix notation
This section describes how to perform all the calculations using matrix variables.

Let $\large X \in \mathbb{R}^{T \times d}$ be the input.

We use a trainable weight matrix $W_q$ which is a concatenation ([[Concatenating matrices|link]]) of matrices $W_q^{(h)}$ per head:
$$
\large
W_q = (W_q^{(1)} \dots W_q^{(H)}) \in \mathbb{R}^{d \times d}, \quad 
W_q^{(h)} \in \mathbb{R}^{d \times d_h}
$$
where:
$$
\large d_h = \frac{d}{H}
$$
to calculate matrix $Q$ which is a concatenation of matrices $Q^{(h)}$ per head:
$$
\large
Q = X W_q = (Q^{(1)} \dots Q^{(H)}) \in \mathbb{R}^{T \times d}, \quad 
Q^{(h)} \in \mathbb{R}^{T \times d_h}
$$
Similarly we have $W_k$ and $W_v$ used to calculate $K$ and $V$.

So:
- Each matrix $W_q^{(h)}, W_k^{(h)}, W_v^{(h)}$ corresponds to a specific head $h$ and is used for every input token
- Each row of $Q^{(h)}, K^{(h)}, V^{(h)}$ corresponds to a specific input token

Then, we break $Q, K, V$ into separate matrices per head $Q^{(h)}, K^{(h)}, V^{(h)}$ so we can calculate weights per head $h$ and each pair of input tokens:
$$
\large
A^{(h)} = \text{softmax}\left( \frac{Q^{(h)} K^{(h)T}} {\sqrt{d_h}} \right)
\in \mathbb{R}^{T \times T}
$$
so $A_{i,j}^{(j)}$ is a weight for the pair of $i$-th an $j$-th input tokens calculated by the head $h$.

And outputs per head $h$ are:
$$
\large Y^{(h)} = A^{(h)} V^{(h)} = \begin{pmatrix}
y_1^{(h)} \\
\vdots \\
y_T^{(h)} \\
\end{pmatrix}
\in \mathbb{R}^{T \times d_h}
$$
Now, concatenate all the outputs:
$$
\large Y_{\text{concat}} = (Y^{(1)} \dots Y^{(H)}) = \begin{pmatrix}
y_1^{\text{concat}} \\
\vdots \\
y_T^{\text{concat}} \\
\end{pmatrix} \in \mathbb{R}^{T \times d}
$$
and calculate the final output using another trainable weight matrix $\large W_o \in \mathbb{R}^{d \times d}$ :
$$
\large Y = Y_{\text{concat}} W_o = \begin{pmatrix}
y_1 \\
\vdots \\
y_T \\
\end{pmatrix} \in \mathbb{R}^{T \times d}
$$
# Comparison to a single-head attention
In a single-head attention:
- One set of matrices $W_q, W_k, W_v$ of shape $(d, d)$ generates one set of matrices $Q, K, V$ of shape $(T, d)$ 
- One set of matrices $Q, K, V$ generates one output matrix $Y$ of shape $(T, d)$ 

In a multi-head attention:
- Each head has its own set of matrices $W^{(h)}_q, W^{(h)}_k, W^{(h)}_v$ of shape $(d, d_h)$ which generates set of matrices $Q^{(h)}, K^{(h)}, V^{(h)}$ of shape $(T, d_h)$ for this head
- One head's set of matrices $Q^{(h)}, K^{(h)}, V^{(h)}$ generates one head's output matrix $y^{(h)}$ of shape $(T, d_h)$ 
- Outputs from all the heads are concatenated to form $\large y^{\text{concat}}$ of shape $(T, d)$ 
- Each row (corresponding to one token) of $\large y^{\text{concat}}$ is multiplied by the matrix $W_o$ to generate the final output $Y$ of shape $(T, d)$ 
# Interpretation
Each head is processing the entire input and is preparing only a part of the final output.

The $i$-th output token (the $i$-th row $Y[i, :]$) can be viewed as a set of features extracted from the $i$-th input token, so we can say, that each head is preparing different features for that output token.

#MachineLearning 