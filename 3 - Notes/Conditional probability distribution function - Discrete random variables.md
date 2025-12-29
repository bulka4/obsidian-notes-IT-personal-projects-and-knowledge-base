Tags: [[__Mathematics]], [[_Probability]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
This document describes how equations and notation for calculating probability using a probability distribution function for multivariate random variables ([[Conditional probability distribution function - Multivariate random variables|link]]) look like in case when that multivariate variable consists only of discrete variables.

In that case, we usually use:
- The Counting measure as $\mu$ 
- $\large \mathcal{Y}_i = \{y_{i1}, y_{i2}, \ldots \}$ - Countable set of all possible values of $Y$ 
- $\large \mathcal{B}_{\mathcal{Y}_i} = 2^{\mathcal{Y}} = \{A: A \subseteq \mathcal{Y}\}$ - Collection of all subsets of $\mathcal{Y}_i$ 

Probability distribution function $\Large p_{Y_{1:n} \mid X_{1:m}}$ can now only return values from the range $[0, 1]$.

The main equations are:
$$
\Large
\begin{align}
 & \Large
P(\bigwedge_{i=1}^n Y_i = y_i \mid \bigwedge_{i=1}^m X_i = x_i) = 
p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m}) \\
 & P(\bigwedge_{i=1}^n Y_i \in A_i \mid \bigwedge_{i=1}^m X_i = x_i) = 
\sum_{y_{1:n} \in \prod_{i=1}^n \mathcal{A}_i} 
p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m}) \\
\end{align}
$$
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
-  $\mu, \mu_i$ - Counting measures:
$$
\large
\mu = \mu_1 \otimes \ldots \otimes \mu_n = \mu_{1:n}^{\otimes n}
$$
- Conditional probability distribution $P_{Y \mid X}$ ([[Conditional probability distribution|link]]) is absolutely continuous with respect to the product measure ([[Product measure|link]]) $\mu$ 
- Both measures $P_{Y \mid X}$ and $\large \mu_{1:n}^{\otimes n}$ are defined on the product space $\large (\prod_{i=1}^n \mathcal{Y}_i, \bigotimes_{i=1}^n \mathcal{B}_{\mathcal{Y}})$ 
- $A$ is a measurable cartesian product ([[Cartesian product|link]], [[Measurable set|link]]):
$$
\large
A = \prod_{i=1}^n A_i,\ A_i = \{y_1, y_2, \ldots \} \subseteq \mathcal{B}_{\mathcal{Y}_i}
$$
- $\large \mathcal{Y}_i = \{y_{i1}, y_{i2}, \ldots \}$ - Countable set of all possible values of $Y$
- $\large \mathcal{B}_{\mathcal{Y}_i} = 2^{\mathcal{Y}} = \{A: A \subseteq \mathcal{Y}\}$ - Collection of all subsets of $\mathcal{Y}_i$ 
# Absolute continuity
Probability distribution $\Large P_{Y_{1:n} \mid X_{1:n}}$ ([[Probability distribution|link]]) for a discrete random variable $Y_{1:n}$ is **always** absolutely continuous with respect to the counting measure $\mu$.
# Integral with the Counting measure
For the Counting measure, we have:
$$
\large
\int_A f(x) d\mu(x) = \sum_{x \in A} f(x)
$$
# Equations
## Equation for the probability of $P(Y_{1:n} \in A)$
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
\sum_{y_1 \in \mathcal{A}_1} \ldots \sum_{y_n \in \mathcal{A}_n}
p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m})
$$
Or in short notation:
$$
\Large
P(\bigwedge_{i=1}^n Y_i \in A_i \mid \bigwedge_{i=1}^m X_i = x_i) = 
\sum_{y_{1:n} \in \prod_{i=1}^n \mathcal{A}_i} 
p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m})
$$
## Equation for probability $Y_i = y_i$
In case when each set contains only one element $A_i = \{y_i\}$, then that equation looks like that:
$$
\Large
P(\bigwedge_{i=1}^n Y_i = y_i \mid \bigwedge_{i=1}^m X_i = x_i) = 
p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m})
$$
## Probability of all possible values
Condition that probability of all possible values equals to 1:
$$
\Large
P_{Y_{1:n} \mid X_{1:m}}(\mathcal{Y} \mid x_{1:m}) = 1
$$
becomes:
$$
\Large
\sum_{y_{1:n} \in \prod_{i=1}^n \mathcal{Y}_i} p_{Y_{1:n}}(y_{1:n}) = 1
$$
## Creating probability mass function formula using probabilities
If we know all probabilities, for all possible values for each variable:
$$
\large
P(\bigwedge_{i=1}^n Y_i = y_i \mid \bigwedge_{i=1}^m X_i = x_i),\ \forall y_{1:n} \in \prod_{i=1}^n \mathcal{Y}_i
$$
then we can use them to create the formula for $\Large p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m})$ in different ways. 

We can use any formula which satisfies:
$$
\Large
p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m}) = P(\bigwedge_{i=1}^n Y_i = y_i \mid \bigwedge_{i=1}^m X_i = x_i)
$$
for example:
$$
\Large
\begin{aligned}
\text{1) } & p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m}) = 
\sum_{y'_{1:n} \in \prod_{i=1}^n \mathcal{Y}_i}
\mathbb{1} \{\bigwedge_{i=1}^n y_i = y'_i\} 
P(\bigwedge_{i=1}^n Y_i = y'_i \mid \bigwedge_{i=1}^m X_i = x_i) \\
\text{2) } & p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m}) = 
\prod_{y'_{1:n} \in \prod_{i=1}^n \mathcal{Y}_i} 
P(\bigwedge_{i=1}^n Y_i = y'_i \mid \bigwedge_{i=1}^m X_i = x_i)
^{ \mathbb{1} \{\bigwedge_{i=1}^n y_i = y'_i\} }
\end{aligned}
$$
where $\mathbb{1} \{y = y'\}$ is indicator function which equals 1 when $y = y'$, otherwise 0.

In case when each variables $Y_i$ are binary (only two possible outcomes $\{0, 1\}$) and independent given $X_i$, we can also specify the probability mass function as:
$$
\Large
p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m}) = \prod_{i=1}^n p_i(x_i)^{y_i} (1 - p_i(x_i))^{1 - y_i},\ y_i \in \{0, 1\}
$$
where $p_i(x_i) = P(Y_i = 1 \mid X_i = x_i)$.

If additionally all the $p_i(x_i) = p$ are the same, then it simplifies to:
$$
\Large
p_{X_{1:n}}(x_{1:n}) = p^{\sum_{i=1}^n x_i} (1 - p)^{n - \sum_{i=1}^n x_i},\ x_i \in \{0, 1\}
$$

All the above forms are equivalent and useful in different scenarios.
## Examples
For example, when we have a random variables:
- $Y: \Omega \rightarrow \mathcal{Y}$ 
- $X: \Omega \rightarrow \mathcal{X} \subset \mathbb{R}$ 
where $\mathcal{Y} = \{y_1, y_2, \ldots \}$ is a set of all possible values for $Y$, then those equations look like that:
$$
\Large
\begin{align}
 & P_{Y \mid X}(A \mid x) = P(Y \in A \mid X = x) = 
\sum_{i=1}^n p_{Y \mid X}(y_i \mid x), \quad A = \{y_i\}_{i=1}^n \\
 & P(Y = y \mid X = x) = p_{Y \mid X}(y \mid x), \quad \forall y \in \mathcal{Y} \\
 & \sum_{i=1}^n p_{Y \mid X}(y \mid x) = 1 \\
 & p_{Y \mid X}(y \mid x) = \sum_{i=1}^n \mathbb{1} \{y = y_i\} P(Y = y_i) \\
 & p_{Y \mid X}(y \mid x) = \prod_{i=1}^n P(Y = y_i)^{ \mathbb{1} \{y = y_i\} } \\
 & p_{Y \mid X}(y \mid x) = p^{y} (1 - p)^{1 - y},\ y \in \{0, 1\} \\
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