Tags: [[__Mathematics]], [[_Probability]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
A multivariate random variable ([[Random variable|link]]) is such a variable, that its output is multi-dimensional. It consists of multiple random variables called components.
# Formal definition
If
- $\mathcal{X} = \mathcal{X}_1 \times \ldots \times \mathcal{X}_n$ - Cartesian product ([[Cartesian product|link]])
- $\mathcal{B}_{\mathcal{X}} = \mathcal{B}_{\mathcal{X}_1} \otimes \ldots \otimes \mathcal{B}_{\mathcal{X}_n}$ - Product $\sigma$-algebra ([[Product sigma algebra|link]]) on $\mathcal{X}$ 

Then $X = (X_1, \ldots, X_n)$ is called a **multivariate** (or **vector**) random variable:
$$
X = (X_1, \ldots, X_n): (\Omega, \mathcal{F}) \rightarrow (\mathcal{X}_1 \times \ldots \times \mathcal{X}_n,\ \mathcal{B}_{\mathcal{X}_1} \otimes \ldots \otimes \mathcal{B}_{\mathcal{X}_n})
$$
Each coordinate projection
$$
\pi_i(x_1, \ldots, x_n) = x_i
$$
gives the **component random variable** $X_i = \pi_i \circ X$:
$$
X_i: (\Omega, \mathcal{F}) \rightarrow (\mathcal{X}_i, \mathcal{B}_{\mathcal{X}_i})
$$
# Further nesting of multivariate variables
We can continue nesting further multivariate variables inside other multivariate variables:
$$
\large
\begin{align}
 & X = (X_1, \ldots, X_{n_1}) \\
 & X_i = (X_{i1}, \ldots, X_{i{n_2}}) \\
 & X_{ij} = (X_{ij1}, \ldots, X_{ij{n_3}}) \\
 & ...
\end{align}
$$
And then $X$ is still considered a multivariate random variable. 

For example we might have two levels of nesting, then $X$ becomes a matrix and represents a table.
# Common example
We usually use:
- $\mathcal{X} = \mathbb{R}^d,\ d \in \mathbb{N}$ 
- $\mathcal{B}_{\mathcal{X}} = \mathcal{B}(\mathbb{R}^d)$ (The Borel $\sigma$-algebra ([[Borel sigma algebra|link]])) 

And then a multivariate random variable is a vector:
$$
X = (X_1, \ldots, X_n): \Omega \rightarrow \mathbb{R}^n
$$
whose each element $X_i$ is a random variable.

A multi-dimensional random variable $X: \Omega \rightarrow \mathbb{R}^d,\ d > 1$ can be represented as a set of separate random variables $X_1, \ldots, X_d$. In that case:
$$
X(\omega) = (X_1(\omega), \ldots, X_d(\omega))
$$
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
# Multivariate random variable vs set of random variables
It is worth to highlight, that:
- Usually when we talk about a set of multiple random variables, we mean a multivariate random variable 
- Considering a set of multiple random variables is equivalent to considering a single, multivariate random variable.
- It is also possible to have a set of multiple random variables where each variable lives in a separate probability spaces and receives a different input $\omega$. In that case, we can't consider all those variables as a single one and we don't call it a multivariate.

More information about it can be found here - [[Multivariate random variable vs set or random variables]].
# Related topics
1. [[Mathematical general notations and shorthands]]
2. [[Random variable]]
3. [[Cartesian product]]
4. [[Product sigma algebra]]
5. [[Borel sigma algebra]]
6. [[Multivariate random variable vs set or random variables]]

#Mathematics #Probability 