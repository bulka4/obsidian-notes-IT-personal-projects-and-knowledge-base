Tags: [[__Mathematics]], [[_Probability]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
This document describes how equations and notation for calculating probability using a probability distribution function for multivariate random variables ([[Conditional probability distribution function - Multivariate random variables|link]]) look like in case when that multivariate variable consists only of continuous variables.

In that case, we usually use:
- The Lebesgue measure ([[Lebesgue measure|link]]) as $\mu$ 
- $\mathcal{X}_i = \mathbb{R}$ 
- $\large \mathcal{B}_{\mathcal{X}_i} = \mathcal{B}(\mathbb{R})$ - Borel -algebra ([[Borel sigma algebra|link]])
# Assumptions
Let's assume that:
- $(\Omega, \mathcal{F}, P)$ - Probability space ([[Probability space (events, probability measure)|link]])
- $X$ is a continuous random variable (can be a multivariate ([[Multivariate random variable|link]]) if n > 1):
$$
\large
X = (X_1, \ldots, X_n): (\Omega, \mathcal{F}) \rightarrow 
(\mathcal{X}, \mathcal{B}_{\mathcal{X}}) = 
(\prod_{i=1}^n \mathcal{X}_i,\ \bigotimes_{i=1}^n \mathcal{B}_{\mathcal{X}_i})
$$
- $\mu, \mu_i$ - Lebesgue measures:
$$
\large
\mu = \mu_1 \otimes \ldots \otimes \mu_n = \mu_{1:n}^{\otimes n}
$$
- Probability distribution $\Large P_{X_{1:n}}$ ([[Probability distribution|link]]) is absolutely continuous with respect to the product measure ([[Product measure|link]]) $\mu$ 
- Both measures $\Large P_{X_{1:n}}$ and $\large \mu_{1:n}^{\otimes n}$ are defined on the product space $\large (\prod_{i=1}^n \mathcal{X}_i,\ \bigotimes_{i=1}^n \mathcal{B}_{\mathcal{X}_i})$ 
- $A$ is a measurable cartesian product ([[Cartesian product|link]], [[Measurable set|link]]):
$$
\large
A = \prod_{i=1}^n A_i,\ A_i = [a_i, b_i] \subseteq \mathbb{R}
$$
- $\mathcal{X}_i = \mathbb{R}$ 
- $\large \mathcal{B}_{\mathcal{X}_i} = \mathcal{B}(\mathbb{R})$ - Borel $\sigma$-algebra ([[Borel sigma algebra|link]])
# Equation for the probability of $P(X_{1:n} \in A)$
The formal equation for probability for a multivariate random variable:
$$
\Large
P(X_{1:n} \in \prod_{i=1}^n A_i) = P(\bigwedge_{i=1}^n X_i \in A_i) = \int_{A_{1:n}} p_{X_{1:n}}(x_{1:n}) d\mu_{n:1}(x_{n:1})
$$
looks like this:
$$
\Large
P(X_{1:n} \in \prod_{i=1}^n A_i) = P(\bigwedge_{i=1}^n X_i \in A_i) = 
\int_{a_1}^{b_1} \ldots \int_{a_n}^{b_n} p_{X_{1:n}}(x_{1:n}) dx_n \ldots dx_1
$$
Or in short:
$$
\Large
P(X_{1:n} \in \prod_{i=1}^n A_i) = P(\bigwedge_{i=1}^n X_i \in A_i) = \int_{a_{1:n}}^{b_{1:n}} p_{X_{1:n}}(x_{1:n}) dx_{n:1}
$$
# Probability of all possible values
Condition that probability of all possible values equals to 1:
$$
\Large
P_{X_{1:n}}(\mathcal{X}) = 1
$$
becomes:
$$
\Large
\int_{\mathbb{R}} \ldots \int_{\mathbb{R}} p_{X_{1:n}}(x_{1:n}) dx_{n:1} = 1
$$
# Examples
For example, if we have a random variable $X: \Omega \rightarrow \mathbb{R}$, then those equations look like that:
$$
\large
\begin{align}
 & P_X(A) = P(X \in A) = \int_a^b p_X(x) dx, \quad A = [a,b]\\
 & P_X(\mathbb{R}) = P(X \in \mathbb{R}) = \int_{\mathbb{R}} p_X(x) dx = 1
\end{align}
$$
# Related topics
1. [[Mathematical general notations and shorthands]]
2. [[Random variable]]
3. [[Probability distribution]]
4. [[Measure]]
5. [[Lebesgue measure]]
6. [[Types of random variables]]
7. [[Counting measure]]
8. [[Probability space (events, probability measure)]]
9. [[Multivariate random variable]]
10. [[Product measure]]
11. [[Cartesian product]]
12. [[Fubini's theorem (multiple integrals)]]

#Mathematics #Probability 