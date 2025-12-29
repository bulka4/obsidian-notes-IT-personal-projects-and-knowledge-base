Tags: [[__Mathematics]], [[_Probability]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
When we have a set of random variables ([[Random variable|link]]) $X_1, \ldots, X_n$, and we know their joint probability distribution ([[Marginal probability distribution|link]]) then we can use **marginalization** in order to obtain marginal joint probability distribution for a subset of those variables, $\large X_I = (X_i)_{i \in I}$ where $I$ is a set of our chosen indexes.
# Formal definition
Let's assume, that:
- $X = (X_1, \ldots, X_n): (\Omega, \mathcal{F}) \rightarrow (\mathcal{X}_1 \times \ldots \times \mathcal{X}_n,\ \mathcal{B}_{\mathcal{X}_1} \otimes \ldots \otimes \mathcal{B}_{\mathcal{X}_n})$ - Multivariate random variable ([[Multivariate random variable|link]])
- $\Large P_{X_{1:n}}$ - Probability distribution ([[Probability distribution|link]]) for $X_1, \ldots, X_n$ 
- $I \subseteq \{1, \ldots, n\}$ - Chosen subset of indexes with $I^c = \{1, \ldots, n\} \setminus I$ as its complement (remaining indexes)

**Marginal probability distribution** of subvector $\large X_I = (X_i)_{i \in I}$ is the pushforward measure of $\Large P_{X_{1:n}}$ under the projection map:
$$
\large
\begin{align}
 & \pi_I: \mathcal{X}_1 \times \ldots \times \mathcal{X}_n \rightarrow \prod_{i \in I} \mathcal{X}_i \\
 & \pi_I (x_1, \ldots, x_n) = (x_i)_{i \in I}
\end{align}
$$
That pushforward measure is defined as:
$$
\Large P_{X_I} = P_{X_{1:n}} \circ \pi_I^{-1}
$$
So we have:
$$
\Large
P_{X_I}(A_I) = P_{X_{1:n}}(\pi_I^{-1}(A_I)),\quad A_I \in \mathcal{B}_{\prod_{i \in I} \mathcal{X}_i}
$$
# Marginal probability distribution function
For a marginal probability distribution there might exist corresponding marginal probability distribution function which allow to represent that distribution using a chosen measure.

More information about it can be found here - [[Marginal probability distribution function]].
# Related topics
1. 

#Mathematics #Probability 