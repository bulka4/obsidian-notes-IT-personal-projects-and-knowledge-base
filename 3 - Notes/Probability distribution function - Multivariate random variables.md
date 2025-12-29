Tags: [[__Mathematics]], [[_Probability]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
This document describes how the equations and notation from the formal definition of the probability distribution function ([[Probability distribution (density, mass) function|link]]) look like in case of multivariate random variables ([[Multivariate random variable|link]]).
# Assumptions
Let's assume, that:
- $(\Omega, \mathcal{F}, P)$ - Probability space ([[Probability space (events, probability measure)|link]])
- $X$ is a multivariate random variable:
$$
\large
X = (X_1, \ldots, X_n): (\Omega, \mathcal{F}) \rightarrow 
(\mathcal{X}, \mathcal{B}_{\mathcal{X}}) = 
(\prod_{i=1}^n \mathcal{X}_i,\ \bigotimes_{i=1}^n \mathcal{B}_{\mathcal{X}_i})
$$
- $\mu$ is a product measure:
$$
\large
\mu = \mu_1 \otimes \ldots \otimes \mu_n = \mu_{1:n}^{\otimes n}
$$
- Probability distribution $P_X$ ([[Probability distribution|link]]) is absolutely continuous with respect to the product measure ([[Product measure|link]]) $\mu$ 
- Both measures $P_X$ and $\large \mu_{1:n}^{\otimes n}$ are defined on the product space $\large (\prod_{i=1}^n \mathcal{X}_i,\ \bigotimes_{i=1}^n \mathcal{B}_{\mathcal{X}_i})$ 
- $A$ is a measurable cartesian product ([[Cartesian product|link]], [[Measurable set|link]]):
$$
\large
A = \prod_{i=1}^n A_i,\ A_i \in \mathcal{B}_{\mathcal{X}_i}
$$
# Probability distribution function notation
For the probability distribution function of a multivariate random variable, we usually use the notation:
$$
\Large
p_{X_1, \ldots, X_n}(x_1, \ldots, x_n)
$$
or in short:
$$
\Large
p_{X_{1:n}}(x_{1:n})
$$
But we can also write $p_X(x)$ as explained further in the [[#Multivariate random variable vs set of random variables]] section in this document.
# Equation for probability $P(X \in A)$
The equation for probability from the formal definition:
$$
P_X(A) = \int_A p_X(x) d\mu(x)
$$
can be written as:
$$
\Large
P_{X_{1:n}}(A) = P(X_{1:n} \in \prod_{i=1}^n A_i) = P(\bigwedge_{i=1}^n X_i \in A_i) = 
\int_{A_1 \times \ldots \times A_n} p_{X_{1:n}}(x_1, \ldots, x_n) d(\mu_1 \otimes \ldots \otimes \mu_n)(x_1, \ldots x_n)
$$
Or in short:
$$
\Large
P(X_{1:n} \in \prod_{i=1}^n A_i) = 
\int_{\prod_{i=1}^n A_i} p_{X_{1:n}}(x_{1:n}) d(\mu^{\otimes n}_{1:n})(x_{1:n})
$$

By Fubini's theorem ([[Fubini's theorem (multiple integrals)|link]]), that equals to:
$$
\Large
P(X_{1:n} \in \prod_{i=1}^n A_i) = \int_{A_1} \ldots \int_{A_n} p_{X_{1:n}}(x_{1:n}) d\mu_n(x_n) \ldots d\mu_1(x_1)
$$
what can be written in short as:
$$
\Large
P(X_{1:n} \in \prod_{i=1}^n A_i) = \int_{A_{1:n}} p_{X_{1:n}}(x_{1:n}) d\mu_{n:1}(x_{n:1})
$$
# Multivariate random variable vs set of random variables
It is worth to highlight, as described here - [[Multivariate random variable vs set or random variables|link]], that considering a single multivariate random variable:
$$
X = (X_1, \ldots, X_n): (\Omega, \mathcal{F}) \rightarrow (\mathcal{X}_1 \times \ldots \times \mathcal{X}_n,\ \mathcal{B}_{\mathcal{X}_1} \otimes \ldots \otimes \mathcal{B}_{\mathcal{X}_n})
$$
Is equivalent to considering a set of different random variables:
$$
\large
X_i: (\Omega, \mathcal{F}) \rightarrow (\mathcal{X}_i, \mathcal{B}_{\mathcal{X}_i})
$$
Those concepts are equivalent and all the formulas and definitions works the same.

For example, probability distribution function $p_X$ of a single, multivariate random variable $X = (X_1, \ldots, X_n)$ is equivalent to a joint probability distribution function of its components $\Large p_{X_{1:n}}$.
# Related topics
1. [[Mathematical general notations and shorthands]]
2. [[Conditional probability distribution (density, mass) function]]
3. [[Probability space (events, probability measure)]]
4. [[Multivariate random variable]]
5. [[Conditional probability distribution]]
6. [[Product measure]]
7. [[Cartesian product]]
8. [[Measurable set]]
9. [[Fubini's theorem (multiple integrals)]]
10. [[Multivariate random variable vs set or random variables]]

#Mathematics #Probability 