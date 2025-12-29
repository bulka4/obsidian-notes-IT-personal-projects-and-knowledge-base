Tags: [[__Mathematics]], [[_Probability]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
This document describes how equations and notation for calculating conditional probability using a conditional probability distribution function for multivariate random variables ([[Conditional probability distribution function - Multivariate random variables|link]]) look like in case when that multivariate variable consists only of continuous variables.

In that case, we usually use:
- The Lebesgue measure ([[Lebesgue measure|link]]) as $\mu$ 
- $\mathcal{X}_i = \mathbb{R}$ 
- $\large \mathcal{B}_{\mathcal{X}_i} = \mathcal{B}(\mathbb{R})$ - Borel -algebra ([[Borel sigma algebra|link]])
# Assumptions
Let's assume that:
- $(\Omega, \mathcal{F}, P)$ - Probability space ([[Probability space (events, probability measure)|link]])
- $Y$ and $X$ are multivariate random variables (can be a multivariate ([[Multivariate random variable|link]]) if n > 1):
$$
\large
\begin{gathered}
Y = (Y_1, \ldots, Y_n): (\Omega, \mathcal{F}) \rightarrow (\prod_{i=1}^n \mathcal{Y}_i, \bigotimes_{i=1}^n \mathcal{B}_{\mathcal{Y}}) \\
X = (X_1, \ldots, X_m): (\Omega, \mathcal{F}) \rightarrow (\prod_{i=1}^m \mathcal{X}_i, \bigotimes_{i=1}^m \mathcal{B}_{\mathcal{X}})
\end{gathered}
$$
-  $\mu, \mu_i$ - Lebesgue measures:
$$
\large
\mu = \mu_1 \otimes \ldots \otimes \mu_n = \mu_{1:n}^{\otimes n}
$$
- Conditional probability distribution $P_{Y \mid X}$ ([[Conditional probability distribution|link]]) is absolutely continuous with respect to the product measure ([[Product measure|link]]) $\mu$ 
- Both measures $P_{Y \mid X}$ and $\large \mu_{1:n}^{\otimes n}$ are defined on the product space $\large (\prod_{i=1}^n \mathcal{Y}_i, \bigotimes_{i=1}^n \mathcal{B}_{\mathcal{Y}})$ 
- $A$ is a measurable cartesian product ([[Cartesian product|link]], [[Measurable set|link]]):
$$
\large
A = \prod_{i=1}^n A_i,\ A_i \subseteq \mathcal{B}_{\mathcal{Y}_i}
$$
- $\mathcal{Y}_i = \mathbb{R}$ 
- $\large \mathcal{B}_{\mathcal{Y}_i} = \mathcal{B}(\mathbb{R})$ - Borel $\sigma$-algebra ([[Borel sigma algebra|link]])
# Equation for the probability of $Y_{1:n} \in A$
The formal equation for probability for a multivariate random variable using a density function:
$$
\Large
P(\bigwedge_{i=1}^n Y_i \in A_i \mid \bigwedge_{i=1}^m X_i = x_i) = 
\int_{A_{1:n}} p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m}) d\mu_{n:1}(y_{n:1})
$$
looks like this:
$$
\Large
P(\bigwedge_{i=1}^n Y_i \in A_i \mid \bigwedge_{i=1}^m X_i = x_i) = 
\int_{a_1}^{b_1} \ldots \int_{a_n}^{b_n} p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m}) dy_n \ldots dy_1
$$
Or in short:
$$
\Large
P(\bigwedge_{i=1}^n Y_i \in A_i \mid \bigwedge_{i=1}^m X_i = x_i) = \int_{a_{1:n}}^{b_{1:n}} p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m}) dy_{n:1}
$$
# Probability of all possible values
Condition that probability of all possible values equals to 1:
$$
\Large
P_{Y_{1:n} \mid X_{1:m}}(\mathcal{Y} \mid x_{1:m}) = 1
$$
becomes:
$$
\Large
\int_{\mathbb{R}} \ldots \int_{\mathbb{R}} p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m}) dy_{n:1} = 1
$$
# Examples
For example, if we have random variables $Y, X: \Omega \rightarrow \mathbb{R}$, then those equations look like that:
$$
\large
\begin{align}
 & P_{Y \mid X}(A \mid x) = P(Y \in A \mid x) = \int_a^b p_{Y \mid X}(y \mid x) dy, \quad A = [a,b]\\
 & P_{Y \mid X}(\mathbb{R}) = P(Y \in \mathbb{R} \mid x) = \int_{\mathbb{R}} p_{Y \mid X}(y \mid x) dy = 1
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