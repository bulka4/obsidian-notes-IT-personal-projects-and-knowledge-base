Tags: [[__Mathematics]], [[_Probability]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
Considering a single multivariate random variable ([[Multivariate random variable|link]]):
$$
X = (X_1, \ldots, X_n): (\Omega, \mathcal{F}) \rightarrow (\mathcal{X}_1 \times \ldots \times \mathcal{X}_n,\ \mathcal{B}_{\mathcal{X}_1} \otimes \ldots \otimes \mathcal{B}_{\mathcal{X}_n})
$$
Is equivalent to considering a set of different random variables:
$$
\large
X_i: (\Omega, \mathcal{F}) \rightarrow (\mathcal{X}_i, \mathcal{B}_{\mathcal{X}_i})
$$
Those concepts are equivalent and all the formulas and definitions works the same.

For example, probability distribution ([[Probability distribution|link]]) $P_X$ of a single, multivariate random variable $X = (X_1, \ldots, X_n)$ is equivalent to a joint probability distribution of its components $\Large P_{X_{1:n}}$.

The same applies to probability distribution functions ([[Probability distribution (density, mass) function|link]]).
# A single probability space as an input
Note, that the input for a multivariate random variable $X = (X_1, \ldots, X_n)$ is $(\Omega, \mathcal{F})$, not $(\Omega, \mathcal{F})^n$. 

So that means that all the component random variables $X_i$ receives the same input:
$$
X(\omega) = (X_1(\omega), \ldots, X_n(\omega)), \quad \omega \in \Omega
$$
So all the random variables lives in the same probability space.

Usually when we talk about multiple random variables, we mean a multivariate random variable, where each component variable $X_i$ receives the same input $\omega$.
# Different probability spaces
It is also possible to consider a set of multiple random variables where each one lives in a different probability space and receive a different input $\omega$ :
$$
X_i: (\Omega_i, \mathcal{F}_i, P_i) \rightarrow (\mathcal{X}_i, \mathcal{B}_{\mathcal{X}_i})
$$
then
$$
X(\omega) = (X_1(\omega_1), \ldots, X_n(\omega_n)), \quad \omega = (\omega_1, \ldots, \omega_n) \in \Omega_1 \times \ldots \times \Omega_n
$$
but in that case, we don't call $X$ a multivariate random variable. We call it a set of random variables from different probability spaces.

Usually when we talk about multiple random variables, we mean a multivariate random variable, where each component variable $X_i$ receives the same input $\omega$.
# Related topics
1. [[Mathematical general notations and shorthands]]
2. [[Multivariate random variable]]
3. [[Probability distribution]]
4. [[Probability distribution (density, mass) function]]

#Mathematics #Probability 