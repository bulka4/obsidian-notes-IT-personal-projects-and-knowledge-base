Tags: [[__Mathematics]], [[_Probability]]

# Introduction

# Formal definition
Let's assume, that:
- $(\Omega, \mathcal{F}, P)$ - Probability space ([[Probability space (events, probability measure)|link]])
- $X: \Omega \rightarrow \mathbb{R}$ - Random variable ([[Random variable|link]])

Expected value of $X$ is defined as:
$$
\mathbb{E}(X) = \int_\Omega X(\omega)dP(\omega)
$$
# Notation
We can also use one of the notations:
$$
\begin{align}
& \mathbb{E}_{X \sim P} \\
& \mathbb{E}_{P(X)} \\
& \mathbb{E}_{P_X}
\end{align}
$$
to indicate that this is an expected value with respect to the random variable $X$ with a probability distribution $P_X$ and probability measure $P$.
# Definition using probability distribution of X
We can also define the expected value of $X$ using its probability distribution ([[Probability distribution|link]]).

Let's assume, that $P_X$ is a probability distribution of $X$, that is:
$$
P_X(A) = P(X \in A), \quad \forall A \in \mathcal{B}(\mathbb{R})
$$
Then, the expected value is defined as:
$$
\mathbb{E}(X) = \int_\mathbb{R} x\ dP_X(x)
$$
## Definition using probability distribution function of X
If there exists a probability distribution function ([[Probability distribution (density, mass) function|link]]) $p_X$ for the probability distribution $P_X$, then formula becomes:
$$
\mathbb{E}(X) = \int_\mathbb{R} x\ p_X(x) dx
$$
# Conditional probability
For conditional probability distribution with the fixed condition $X = x$, we have equivalent definitions:
$$
\large
\begin{align}
 & \mathbb{E}_{P(Y \mid X = x)}(Y) = \int_\mathbb{R} y\ dP_{Y \mid X = x}(y) \\
 & \mathbb{E}_{P(Y \mid X = x)}(Y) = \int_\mathbb{R} y\ p_{Y \mid X = x}\ dy
\end{align}
$$

# Expected value for different types of random variables
This section describes how the expected value formula looks like in case of different types of random variables ([[Types of random variables|link]]):
- Discrete
- Continuous
## Discrete random variables
In case when $X$ is a discrete random variable and:
-  $\large \mathcal{X} = \{x_i\}_{i \ge 0}$ - Set of all possible values of $X$ 
- $P_X(\{x_k\}) = p_k,\ \forall x_K \in \mathcal{X}$ 

$P_X$ is always absolutely continuous with respect to the Counting measure ([[Counting measure|link]]) $\mu$, so that is such a measure that:
$$
\mu(A) = |A| \text{ - number of elements in } A
$$
Then, by the Radon-Nikodym theorem, we have:
$$
dP_X(x) = p(x)d\mu(x)
$$
so:
$$
\mathbb{E}(X) = \int_\mathbb{R} x\ p(x) d\mu(x)
$$
Because $\mu$ is the Counting measure, the integral becomes a sum:
$$
\large
\mathbb{E}(X) = \sum_{x \in \mathcal{X}} x\ p(x)
$$
## Continuous random variables
If $P_X$ is absolutely continuous w.r.t the Lebesgue measure ([[Lebesgue measure|link]]) $\lambda$, then, by the Radon-Nikodym theorem, there exists a density function $f$ such that:
$$
dP_X(x) = f(x) d\lambda(X)
$$
so:
$$
\mathbb{E}(X) = \int_\mathbb{R} x f(x) d\lambda(x)
$$
what can be written as:
$$
\mathbb{E}(X) = \int_{-\infty}^\infty x f(x) dx
$$
# Related topics
1. 

#Mathematics #Probability 