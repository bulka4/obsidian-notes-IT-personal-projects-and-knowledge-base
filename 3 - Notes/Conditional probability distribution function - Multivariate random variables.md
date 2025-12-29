Tags: [[__Mathematics]], [[_Probability]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
This document describes how the equations and notation from the formal definition of the conditional probability distribution function ([[Conditional probability distribution (density, mass) function|link]]) look like in case of multivariate random variables ([[Multivariate random variable|link]]).
# Assumptions
Let's assume, that:
- $(\Omega, \mathcal{F}, P)$ - Probability space ([[Probability space (events, probability measure)|link]])
- $Y$ and $X$ are multivariate random variables:
$$
\begin{gathered}
Y = (Y_1, \ldots, Y_n): (\Omega, \mathcal{F}) \rightarrow (\mathcal{Y}_1 \times \ldots \times \mathcal{Y}_n,\ \mathcal{B}_{\mathcal{Y}_1} \otimes \ldots \otimes \mathcal{B}_{\mathcal{Y}_n}) \\
X = (X_1, \ldots, X_m): (\Omega, \mathcal{F}) \rightarrow (\mathcal{X}_1 \times \ldots \times \mathcal{X}_m,\ \mathcal{B}_{\mathcal{X}_1} \otimes \ldots \otimes \mathcal{B}_{\mathcal{X}_m})
\end{gathered}
$$
- $\mu$ is a product measure:
$$
\large
\mu = \mu_1 \otimes \ldots \otimes \mu_n = \mu_{1:n}^{\otimes n}
$$
- Conditional probability distribution $P_{Y \mid X}$ ([[Conditional probability distribution|link]]) is absolutely continuous with respect to the product measure ([[Product measure|link]]) $\mu$ 
- Both measures $P_{Y \mid X}$ and $\large \mu_{1:n}^{\otimes n}$ are defined on the product space $\large (\prod_{i=1}^n \mathcal{Y}_i,\ \bigotimes_{i=1}^n \mathcal{B}_{\mathcal{Y}_i})$ 
- $A$ is a measurable cartesian product ([[Cartesian product|link]], [[Measurable set|link]]):
$$
\large
A = \prod_{i=1}^n A_i,\ A_i \subseteq \mathcal{B}_{\mathcal{Y}_i}
$$
# Probability distribution function notation
For the probability distribution function we usually use the notation:
$$
\Large
p_{Y_1, \ldots, Y_n \mid X_1, \ldots, X_m}(y_1, \ldots, y_n \mid x_1, \ldots, x_m)
$$
or in short:
$$
\Large
p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m})
$$
But we can also write $p_{Y \mid X}(y \mid x)$ as explained further in the [[#Multivariate random variable vs set of random variables]] section in this document.
# Equation for probability $P(X \in A)$
The equation for probability from the formal definition:
$$
P_{Y \mid X}(A \mid x) = \int_A p_{Y \mid X}(y \mid x) d\mu(y)
$$
can be written as:
$$
\Large
P_{Y_{1:n} \mid X_{1:m}}(A \mid x_1, \ldots, x_m) = P(Y_{1:n} \in A \mid \bigwedge_{i=1}^m X_i = x_i) = P(\bigwedge_{i=1}^n Y_i \in A_i \mid \bigwedge_{i=1}^m X_i = x_i) = 
\int_{A_1 \times \ldots \times A_n} p_{Y_{1:n} \mid X_{1:m}}(y_1, \ldots, y_n \mid x_1, \ldots, x_m) d(\mu_1 \otimes \ldots \otimes \mu_n)(y_1, \ldots y_n)
$$
Or in short:
$$
\Large
P(\bigwedge_{i=1}^n Y_i \in A_i \mid \bigwedge_{i=1}^m X_i = x_i) = 
\int_{\prod_{i=1}^n A_i} p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m}) d(\mu^{\otimes n}_{1:n})(y_{1:n})
$$

By Fubini's theorem ([[Fubini's theorem (multiple integrals)|link]]), that equals to:
$$
\Large
P(\bigwedge_{i=1}^n Y_i \in A_i \mid \bigwedge_{i=1}^m X_i = x_i) = 
\int_{A_1} \ldots \int_{A_n} p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m}) d\mu_n(y_n) \ldots d\mu_1(y_1)
$$
what can be written in short as:
$$
\Large
P(\bigwedge_{i=1}^n Y_i \in A_i \mid \bigwedge_{i=1}^m X_i = x_i) = 
\int_{A_{1:n}} p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m}) d\mu_{n:1}(y_{n:1})
$$
# Multivariate random variable vs set of random variables
It is worth to highlight, as described here - [[Multivariate random variable vs set or random variables|link]], that considering a single multivariate random variable:
$$
Y = (Y_1, \ldots, Y_n): (\Omega, \mathcal{F}) \rightarrow (\mathcal{Y}_1 \times \ldots \times \mathcal{Y}_n,\ \mathcal{B}_{\mathcal{Y}_1} \otimes \ldots \otimes \mathcal{B}_{\mathcal{Y}_n})
$$
Is equivalent to considering a set of different random variables:
$$
\large
Y_i: (\Omega, \mathcal{F}) \rightarrow (\mathcal{Y}_i, \mathcal{B}_{\mathcal{Y}_i})
$$
Those concepts are equivalent and all the formulas and definitions works the same.

For example, probability distribution function $p_{Y \mid X}$ of a single, multivariate random variable $Y = (Y_1, \ldots, Y_n)$ is equivalent to a joint probability distribution function of its components $\Large p_{Y_{1:n} \mid X_{1:m}}$.
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