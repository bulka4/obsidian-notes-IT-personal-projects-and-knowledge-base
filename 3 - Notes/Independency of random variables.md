Tags: [[__Mathematics]], [[_Probability]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
This document describes the concept of independency of random variables in two sections:
- **General, formal definition** - Definition expressed in terms of a probability distribution ([[Product measure|link]])
- **Relation to probability and probability distribution function** - What equations are implicated by the independency of random variables in terms of probability and probability distribution function.

It also covers the case of a conditional probability.
# General, formal definition
We define random variable $X_1, \ldots, X_n$ to be independent if and only if
$$
\Large
P_{X_{1:n}}(\prod_{i=1}^n A_i) = \prod_{i=1}^n P_{X_i}(A_i), \quad \forall A_i \in \mathcal{B}_{\mathcal{X}_i}
$$
where:
- $X_{1:n} = (X_1, \ldots, X_n): (\Omega, \mathcal{F}) \rightarrow (\mathcal{X}_1 \times \ldots \times \mathcal{X}_n,\ \mathcal{B}_{\mathcal{X}_1} \otimes \ldots \otimes \mathcal{B}_{\mathcal{X}_n})$ - Multivariate random variable
- $\Large P_{X_{1:n}}$ - Probability distribution ([[Probability distribution|link]]) of $X = (X_1, \ldots, X_n)$ 

So that means, that $\Large P_{X_{1:n}}$ is a product measure:
$$
\Large 
P_{X_{1:n}} = \bigotimes_{i=1}^n P_{X_i} = P_{X_1} \otimes \ldots \otimes P_{X_n}
$$
on the product measurable space:
$$
(\mathcal{X}_1 \times \ldots \times \mathcal{X}_n,\ \mathcal{B}_{\mathcal{X}_1} \otimes \ldots \otimes \mathcal{B}_{\mathcal{X}_n})
$$
## Conditional probability
We say that random variables $Y_i$ are independent given $\large X_{1:n}$ if and only if:
$$
\Large
P_{Y_{1:n} \mid X_{1:n}}(\prod_{i=1}^n A_i) = \prod_{i=1}^n P_{Y_i \mid X_{1:n}}(A_i), \quad \forall A_i \in \mathcal{B}_{\mathcal{Y}_i}
$$
### Case when $Y_i$ depends only on the corresponding $X_i$
If we additionally assume that each $Y_i$ depends only on the corresponding $X_i$, that means:
$$
\Large
P_{Y_i \mid X_{1:n}} = P_{Y_i \mid X_i}
$$
then the equation simplifies to:
$$
\Large
P_{Y_{1:n} \mid X_{1:n}}(\prod_{i=1}^n A_i) = \prod_{i=1}^n P_{Y_i \mid X_i}(A_i), \quad \forall A_i \in \mathcal{B}_{\mathcal{Y}_i}
$$
# Relation to probability and probability distribution function
Let's remind, that probability distribution is used to calculate probabilities:
$$
P_X(A) = P(X \in A)
$$
and that for a probability distribution there exists a probability distribution function $p_X$ if $P_X$ is absolutely continuous w.r.t a chosen measure $\mu$. This function satisfies:
$$
P_X(A) = \int_A p_X(x) d\mu(x)
$$

So equations for independency of random variables can be written as:
$$
\Large
\begin{align}
 & p_{X_{1:n}}(\prod_{i=1}^n A_i) = \prod_{i=1}^n p_{X_i}(A_i) \\
 & P(X_{1:n} \in \prod_{i=1}^n A_i) = P(X_1 \in A_1 \wedge \ldots \wedge X_n \in A_n)
 = \prod_{i=1}^n P(X_i \in A_i)
\end{align}
$$
for any $\large A_i \in \mathcal{B}_{\mathcal{X}_i}$.

We have the equivalent equations for a conditional probability.
# Related topics
1. [[Random variable]]
2. 

#Mathematics #Probability 