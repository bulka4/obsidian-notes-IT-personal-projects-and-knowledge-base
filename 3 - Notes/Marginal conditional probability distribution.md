Tags: [[__Mathematics]], [[_Probability]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
When we have a set of random variables ([[Random variable|link]]) $Y_1, \ldots, Y_n$, and we know their conditional probability distribution ([[Marginal conditional probability distribution|link]]) given other random variable $X$ then we can use **marginalization** in order to obtain marginal conditional probability distribution for a subset of those variables, $\large Y_I = (Y_i)_{i \in I}$ where $I$ is a set of our chosen indexes.
# Formal definition
Let's assume, that:
- We have multivariate random variables ([[Multivariate random variable|link]]):
	- $Y = (Y_1, \ldots, Y_n): (\Omega, \mathcal{F}) \rightarrow (\mathcal{Y}_1 \times \ldots \times \mathcal{Y}_n,\ \mathcal{B}_{\mathcal{Y}_1} \otimes \ldots \otimes \mathcal{B}_{\mathcal{Y}_n})$ 
	- $X = (X_1, \ldots, X_m): (\Omega, \mathcal{F}) \rightarrow (\mathcal{X}_1 \times \ldots \times \mathcal{X}_m,\ \mathcal{B}_{\mathcal{X}_1} \otimes \ldots \otimes \mathcal{B}_{\mathcal{X}_m})$
- $\Large P_{Y_{1:n} \mid X_{1:m}}$ - Conditional probability distribution of $\large Y_{1:n}$ given $\large X_{1:m}$ ([[Probability distribution|link]]) 
-  $I \subseteq \{1, \ldots, n\}$ - Chosen subset of indexes with $I^c = \{1, \ldots, n\} \setminus I$ as its complement (remaining indexes)

**Marginal conditional probability distribution** of subvector $\large Y_I = (Y_i)_{i \in I}$ given $\large X_{1:m}$, is the pushforward measure of $\Large P_{Y_{1:n} \mid X_{1:m}}$ under the projection map:
$$
\large
\begin{align}
 & \pi_I: \mathcal{Y}_1 \times \ldots \times \mathcal{Y}_n \rightarrow \prod_{i \in I} \mathcal{Y}_i \\
 & \pi_I (y_1, \ldots, y_n) = (y_i)_{i \in I}
\end{align}
$$
That pushforward measure is:
$$
\Large P_{Y_I \mid X_{1:m}} = P_{Y_{1:n} \mid X_{1:m}} \circ \pi_I^{-1}
$$
So we have:
$$
\Large P_{Y_I \mid X_{1:m}}(A_I) = P_{Y_{1:n} \mid X_{1:m}}(\pi_I^{-1}(A_I)),\quad A_I \in \mathcal{B}_{\prod_{i \in I} \mathcal{Y}_i}
$$
# Marginal conditional probability distribution function
For a marginal conditional probability distribution there might exist corresponding marginal conditional probability distribution function which allow to represent that distribution using a chosen measure.

More information about it can be found here - [[Marginal conditional probability distribution function]].
# Related topics
1. 

#Mathematics #Probability 