Tags: [[__Machine_Learning]]

# Introduction
We say that a sequence of random variables $X_1, \ldots, X_n$ are independent and identically distributed (i.i.d in short) if the following conditions as satisfied:

**1. Independency**
For any subset of indexes $\{i_1, \ldots, i_k\} \subseteq \{1, \ldots, n\}$, we have:
$$
\large
P(X_{i_1} \in A_1 \wedge \ldots \wedge X_{i_k} \in A_k) = \prod_{j=1}^k P(X_{i_j} \in A_j)
$$
for any measurable sets $A_i$.

**2. Identical distribution**
Each random variable $X_i$ has the same probability distribution ([[Probability distribution|link]]).
# Common, generic random variable
When we have i.i.d. random variables $X_1, \ldots, X_n$, we can look at them as copies or samples of a common, generic random variable $X$ .

We can say that $X$ is unknown, true random variable which generated given dataset of observations ([[Dataset of observations of random variable X - Variables per sample and variable|link]]), and $X_i$ are its copies which generated each of sample from that dataset.
# More information on independency of random variables
More information on independency of random variables can be found here - [[Independency of random variables]].

#MachineLearning 