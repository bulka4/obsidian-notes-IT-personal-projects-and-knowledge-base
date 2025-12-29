Tags: [[__Machine_Learning]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
We say that a sequence of pairs of random variables $((X_1, Y_1), \ldots, (X_n, Y_n))$ are independent and identically distributed (in short we say that pairs $(X_i, Y_i)$ are i.i.d.) if the following conditions as satisfied:

**1. Independency**
For any subset of indexes $\{i_1, \ldots, i_k\} \subseteq \{1, \ldots, n\}$, we have:
$$
\large
P(\bigwedge_{j=1}^k Y_{i_j} \in A_j \mid \bigwedge_{i=1}^n X_i = x_i) = 
\prod_{j=1}^k P(Y_{i_j} \in A_j \mid \bigwedge_{i=1}^n X_i = x_i)
$$
for any measurable sets $A_i$.

**2. Identical distribution**
Each random variable $Y_i$ has the same probability distribution ([[Probability distribution|link]]). Also $X_i$ have the same distribution (but might be different then $Y_i$).
# $Y_i$ depends only on the corresponding $X_i$
If we additionally assume, that each $Y_i$ depends only on the corresponding $X_i$, then we have:
$$
P(Y_i \in A_i \mid \bigwedge_{j=1}^n X_j = x_j) = P(Y_i \in A_i \mid X_i = x_i)
$$
So the formula from independency simplifies:
$$
\large
P(\bigwedge_{j=1}^k Y_{i_j} \in A_j \mid \bigwedge_{i=1}^n X_i = x_i) = 
\prod_{j=1}^k P(Y_{i_j} \in A_j \mid X_{i_j} = x_{i_j})
$$
# More information on independency of random variables
More information on independency of random variables can be found here - [[Independency of random variables]].
# Common terminology and assumptions
Usually when we work with pairs of random variables $(X_i, Y_i)$, we use assumptions and terminology as described here - [[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable]].

#MachineLearning 