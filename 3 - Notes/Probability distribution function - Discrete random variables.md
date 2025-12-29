Tags: [[__Mathematics]], [[_Probability]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
This document describes how equations and notation for calculating probability using a probability distribution function for multivariate random variables ([[Probability distribution function - Multivariate random variables|link]]) look like in case when that multivariate variable consists only of discrete variables.

In that case, we usually use:
- The Counting measure as $\mu$
- $\large \mathcal{X}_i = \{x_{i1}, x_{i2}, \ldots \}$ - Countable set of all possible values of $X$ 
- $\large \mathcal{B}_{\mathcal{X}_i} = 2^{\mathcal{X}} = \{A: A \subseteq \mathcal{X}\}$ - Collection of all subsets of $\mathcal{X}_i$ 

Probability distribution function $\Large p_{X_{1:n}}$ can now only return values from the range $[0, 1]$.

The main equations are:
$$
\large
\begin{align}
 & P(\bigwedge_{i=1}^n X_i = x_i) = p_{X_{1:n}}(x_{1:n}) \\
 & P(\bigwedge_{i=1}^n X_i \in A_i) = 
\sum_{x_{1:n} \in \prod_{i=1}^n A_i} p_{X_{1:n}}(x_{1:n}) \\
\end{align}
$$
# Assumptions
Let's assume that:
- $(\Omega, \mathcal{F}, P)$ - Probability space ([[Probability space (events, probability measure)|link]])
- $X$ is a discrete random variable (can be a multivariate ([[Multivariate random variable|link]]) if n > 1):
$$
\large
X = (X_1, \ldots, X_n): (\Omega, \mathcal{F}) \rightarrow 
(\mathcal{X}, \mathcal{B}_{\mathcal{X}}) = 
(\prod_{i=1}^n \mathcal{X}_i,\ \bigotimes_{i=1}^n \mathcal{B}_{\mathcal{X}_i})
$$
- $\mu, \mu_i$ - Counting measures:
$$
\large
\mu = \mu_1 \otimes \ldots \otimes \mu_n = \mu_{1:n}^{\otimes n}
$$
- Both measures $\Large P_{X_{1:n}}$ and $\large \mu_{1:n}^{\otimes n}$ are defined on the product space $\large (\prod_{i=1}^n \mathcal{X}_i,\ \bigotimes_{i=1}^n \mathcal{B}_{\mathcal{X}_i})$ 
- $A$ is a measurable cartesian product ([[Cartesian product|link]], [[Measurable set|link]]):
$$
\large
A = \prod_{i=1}^n A_i,\ A_i = \{x_1, x_2, \ldots \} \subseteq \mathcal{B}_{\mathcal{X}_i}
$$
- $\large \mathcal{X}_i = \{x_{i1}, x_{i2}, \ldots \}$ - Countable set of all possible values of $X$
- $\large \mathcal{B}_{\mathcal{X}_i} = 2^{\mathcal{X}} = \{A: A \subseteq \mathcal{X}\}$ - Collection of all subsets of $\mathcal{X}_i$ 
# Absolute continuity
Probability distribution $\Large P_{X_{1:n}}$ ([[Probability distribution|link]]) for a discrete random variable $X_{1:n}$ is **always** absolutely continuous with respect to the counting measure $\mu$.
# Integral with the Counting measure
For the Counting measure $\mu$, we have:
$$
\large
\int_A f(x) d\mu(x) = \sum_{x \in A} f(x)
$$
# Equations
## Equation for the probability of $P(X_{1:n} \in A)$
So the formal equation for probability for a multivariate random variable:
$$
\Large
P(X_{1:n} \in \prod_{i=1}^n A_i) = P(\bigwedge_{i=1}^n X_i \in A_i) = \int_{A_{1:n}} p_{X_{1:n}}(x_{1:n}) d\mu_{n:1}(x_{n:1})
$$
looks like this:
$$
\large
P(X_{1:n} \in \prod_{i=1}^n A_i) = P(\bigwedge_{i=1}^n X_i \in A_i) = 
\sum_{x_1 \in A_1} \ldots \sum_{x_n \in A_n}
p_{X_{1:n}}(x_1, \ldots, x_n)
$$
Or in short:
$$
\Large
P(X_{1:n} \in \prod_{i=1}^n A_i) = P(\bigwedge_{i=1}^n X_i \in A_i) = 
\sum_{x_{1:n} \in \prod_{i=1}^n A_i} p_{X_{1:n}}(x_{1:n})
$$
## Equation for probability $X_i = x_i$
In case when each set contains only one element $A_i = \{x_i\}$, then that equation looks like that:
$$
\Large
P_{X_{1:n}}(A) = P(X_{1:n} \in \prod_{i=1}^n A_i) = P(\bigwedge_{i=1}^n X_i = x_i) = p_{X_{1:n}}(x_{1:n})
$$
## Probability of all possible values
Condition that probability of all possible values equals to 1:
$$
\Large
P_{X_{1:n}}(\mathcal{X}) = 1
$$
becomes:
$$
\Large
\sum_{x_{1:n} \in \prod_{i=1}^n \mathcal{X}_i} p_{X_{1:n}}(x_{1:n}) = 1
$$
## Creating probability mass function formula using probabilities
If we know all probabilities, for all possible values for each variable:
$$
\large
P(\bigwedge_{i=1}^n X_i = x_i),\ \forall x_{1:n} \in \prod_{i=1}^n \mathcal{X}_i
$$
then we can use them to create the formula for $\Large p_{X_{1:n}}(x_{1:n})$ in different ways.

We can use any formula which satisfies:
$$
\Large
p_{X_{1:n}}(x_{1:n}) = P(\bigwedge_{i=1}^n X_i = x_i)
$$
for example:
$$
\Large
\begin{aligned}
\text{1) } & p_{X_{1:n}}(x_{1:n}) = 
\sum_{x'_{1:n} \in \prod_{i=1}^n \mathcal{X}_i}
\mathbb{1} \{\bigwedge_{i=1}^n x_i = x'_i\} 
P(\bigwedge_{i=1}^n X_i = x'_i) \\
\text{2) } & p_{X_{1:n}}(x_{1:n}) = 
\prod_{x'_{1:n} \in \prod_{i=1}^n \mathcal{X}_i} 
P(\bigwedge_{i=1}^n X_i = x'_i)
^{ \mathbb{1} \{\bigwedge_{i=1}^n x_i = x'_i\} }
\end{aligned}
$$
where $\mathbb{1} \{x = x'\}$ is indicator function which equals 1 when $x = x'$, otherwise 0.

In case when each variables $X_i$ are binary (only two possible outcomes $\{0, 1\}$) and independent on each other, we can also specify the probability mass function as:
$$
\Large
p_{X_{1:n}}(x_{1:n}) = \prod_{i=1}^n p_i^{x_i} (1 - p_i)^{1 - x_i},\ x_i \in \{0, 1\}
$$
where $p_i = P(X_i = 1)$.

If additionally all the $p_i = p$ are the same, then it simplifies to:
$$
\Large
p_{X_{1:n}}(x_{1:n}) = p^{\sum_{i=1}^n x_i} (1 - p)^{n - \sum_{i=1}^n x_i},\ x_i \in \{0, 1\}
$$

All the above forms are equivalent and useful in different scenarios.
## Examples
For example, when we have a random variable $X: \Omega \rightarrow \mathcal{X}$, where $\mathcal{X} = \{x_1, x_2, \ldots \}$ is a set of all possible values for $X$, then those equations look like that:
$$
\Large
\begin{align}
 & P_X(A) = P(X \in A) = 
\sum_{i=1}^n p_X(x_i), \quad A = \{x_i\}_{i=1}^n \\
 & P(X = x) = p_X(x), \quad \forall x \in \mathcal{X} \\
 & \sum_{i=1}^n p_X(x_i) = 1 \\
 & p_X(x) = \sum_{i=1}^n \mathbb{1} \{x = x_i\} P(X = x_i) \\
 & p_X(x) = \prod_{i=1}^n P(X = x_i)^{ \mathbb{1} \{x = x_i\} } \\
 & p_X(x) = p^{x} (1 - p)^{1 - x},\ x \in \{0, 1\} \\
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