Tags: [[__Mathematics]], [[_Probability]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
This document describes how equations and notation for calculating probability using a probability distribution function for multivariate random variables ([[Conditional probability distribution function - Multivariate random variables|link]]) look like in case when that multivariate variable consists of both continuous and discrete variables.

In that case, we usually use:
- A product measure which is a mix of the Counting and Lebesgue measures as $\mu$ :
$$
\mu = \bigotimes_{d \in D} \upsilon_d \otimes \bigotimes_{c \in C} \lambda_c
$$
- when $i \in D$ :
	- $\large \mathcal{X}_i = \{x_{i1}, x_{i2}, \ldots \}$ - Countable set of all possible values of $X$ 
	- $\large \mathcal{B}_{\mathcal{X}_i} = 2^{\mathcal{X}} = \{A: A \subseteq \mathcal{X}\}$ - Collection of all subsets of $\mathcal{X}_i$ 
- When $i \in C$ :
	- $\mathcal{X}_i = \mathbb{R}$ 
	- $\large \mathcal{B}_{\mathcal{X}_i} = \mathcal{B}(\mathbb{R})$ - Borel $\sigma$-algebra ([[Borel sigma algebra|link]])
# Assumptions
Let's assume that:
- $(\Omega, \mathcal{F}, P)$ - Probability space ([[Probability space (events, probability measure)|link]])
- $X = (X_D, X_C)$ is a mix of continuous and discrete random variables, where:
	- $X_D = (X_d)_{d \in D}$ - Discrete random variable (can be a multivariate)
	- $X_C = (X_c)_{c \in C}$ - Continuous random variable (can be a multivariate)
	- $D, C$ - Disjoint sets of indexes of discrete (D) and continuous (C) random variables ($D \cup C = \{1, \ldots, n\}$)
$$
\large
X = (X_D, X_C): (\Omega, \mathcal{F}) \rightarrow 
(\mathcal{X}, \mathcal{B}_{\mathcal{X}}) = 
(\prod_{d \in D} \mathcal{X}_d \times \prod_{c \in C} \mathcal{X}_c, \bigotimes_{d \in D} \mathcal{B}_{\mathcal{X}_d} \otimes \bigotimes_{c \in C} \mathcal{B}_{\mathcal{X}_c})
$$
- $\mu$ is a product measure which is a mix of the Counting $\upsilon_d$ and Lebesgue measures $\lambda_c$:
$$
\mu = \bigotimes_{d \in D} \upsilon_d \otimes \bigotimes_{c \in C} \lambda_c
$$
- Joint probability distribution $\Large P_{X_{1:n}}$ is absolutely continuous w.r.t the measure $\mu$ 
- Both measures $\Large P_{X_{1:n}}$ and $\mu$ are defined on the product measurable space:
$$
\large (\prod_{d \in D} \mathcal{X}_d \times \prod_{c \in C} \mathcal{X}_c, \bigotimes_{d \in D} \mathcal{B}_{\mathcal{X}_d} \otimes \bigotimes_{c \in C} \mathcal{B}_{\mathcal{X}_c})
$$
- $A$ is a measurable cartesian product ([[Cartesian product|link]], [[Measurable set|link]]):
$$
\large
\begin{align}
 & A = \prod_{c \in C} A_c \times \prod_{d \in D} A_d \\
 & A_c = [a_c, b_c] \subseteq \mathbb{R} \\
 & A_d = \{x_{d1}, x_{d2}, \ldots\} \subseteq 2^\mathcal{X}
\end{align}
$$
- when $i \in D$ :
	- $\large \mathcal{X}_i = \{x_{i1}, x_{i2}, \ldots \}$ - Countable set of all possible values of $X$ 
	- $\large \mathcal{B}_{\mathcal{X}_i} = 2^{\mathcal{X}} = \{A: A \subseteq \mathcal{X}\}$ - Collection of all subsets of $\mathcal{X}_i$ 
- When $i \in C$ :
	- $\mathcal{X}_i = \mathbb{R}$ 
	- $\large \mathcal{B}_{\mathcal{X}_i} = \mathcal{B}(\mathbb{R})$ - Borel $\sigma$-algebra ([[Borel sigma algebra|link]])
- $I \subseteq D \cup C$ - Subset of variable indexes with $I^c$ as its complement
- $I_d = I \cap D$ - Subset of indexes for discrete variables
- $I_c = I \cap C$ - Subset of indexes for continuous variables
- $I^c_c, I^c_d$ - Complements of $I_c, I_d$ 
# Equation for the probability of $P(X_{1:n} \in A)$
Then, for the formal equation for probability for a multivariate random variable:
$$
\Large
P(X_{1:n} \in \prod_{i=1}^n A_i) = P(\bigwedge_{i=1}^n X_i \in A_i) = \int_{A_{1:n}} p_{X_{1:n}}(x_{1:n}) d\mu_{n:1}(x_{n:1})
$$
we have:
$$
\Large
\int_{A_i} p_{X_{1:n}}(x_{1:n}) d\mu_i(x_i) = 
\begin{cases}
\int_{A_i} p_{X_{1:n}}(x_{1:n}) dx_i, \text{ if } X_i \text{ - continuous} \\
\sum_{x_i \in A_i} p_{X_{1:n}}(x_{1:n}), \text{ if } X_i \text{ - discrete}
\end{cases}
$$
So that equation looks like that:
$$
\Large
\begin{align}
 & P_{X_{1:n}}(\prod_{c \in C} A_c \times \prod_{d \in D} A_d) = 
P(X_C \in \prod_{c \in C} A_c \wedge X_D \in \prod_{d \in D} A_d) = \\
 & \quad = \sum_{x_D \in \prod_{d \in D} A_d} \int_{\prod_{c \in C} A_c} 
 p_{X_{1:n}}(x_C, x_D) dx_C
\end{align}
$$
where $\large x_D = (x_d)_{d \in D}$ .
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