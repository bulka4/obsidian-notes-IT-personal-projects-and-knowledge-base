Tags: [[__Mathematics]], [[_Probability]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
This document describes how equations and notation for calculating conditional probability using a conditional probability distribution function for multivariate random variables ([[Conditional probability distribution function - Multivariate random variables|link]]) look like in case when that multivariate variable consists of both continuous and discrete variables.

In that case, we usually use:
- A product measure which is a mix of the Counting and Lebesgue measures as $\mu$ :
$$
\mu = \bigotimes_{d \in D} \upsilon_d \otimes \bigotimes_{c \in C} \lambda_c
$$
- when $i \in D$ :
	- $\large \mathcal{Y}_i = \{y_{i1}, y_{i2}, \ldots \}$ - Countable set of all possible values of $Y$ 
	- $\large \mathcal{B}_{\mathcal{Y}_i} = 2^{\mathcal{Y}} = \{A: A \subseteq \mathcal{Y}\}$ - Collection of all subsets of $\mathcal{Y}_i$ 
- When $i \in C$ :
	- $\mathcal{Y}_i = \mathbb{R}$ 
	- $\large \mathcal{B}_{\mathcal{Y}_i} = \mathcal{B}(\mathbb{R})$ - Borel $\sigma$-algebra ([[Borel sigma algebra|link]])
# Assumptions
Let's assume that:
- $(\Omega, \mathcal{F}, P)$ - Probability space ([[Probability space (events, probability measure)|link]])
- $Y = (Y_D, Y_C)$ is a mix of continuous and discrete random variables, where:
	- $Y_D = (Y_d)_{d \in D}$ - Discrete random variable (can be a multivariate)
	- $Y_C = (Y_c)_{c \in C}$ - Continuous random variable (can be a multivariate)
	- $D, C$ - Disjoint sets of indexes of discrete (D) and continuous (C) random variables ($D \cup C = \{1, \ldots, n\}$)
$$
\large
Y = (Y_D, Y_C): (\Omega, \mathcal{F}) \rightarrow 
(\mathcal{Y}, \mathcal{B}_{\mathcal{Y}}) = 
(\prod_{d \in D} \mathcal{Y}_d \times \prod_{c \in C} \mathcal{Y}_c, \bigotimes_{d \in D} \mathcal{B}_{\mathcal{Y}_d} \otimes \bigotimes_{c \in C} \mathcal{B}_{\mathcal{Y}_c})
$$
- $\mu$ is a product measure which is a mix of the Counting $\upsilon_d$ and Lebesgue measures $\lambda_c$:
$$
\mu = \bigotimes_{d \in D} \upsilon_d \otimes \bigotimes_{c \in C} \lambda_c
$$
- Joint probability distribution $\Large P_{Y_{1:n} \mid X_{1:m}}$ is absolutely continuous w.r.t the measure $\mu$ 
- Both measures $\Large P_{Y_{1:n} \mid X_{1:m}}$ and $\mu$ are defined on the product measurable space:
$$
\large
(\prod_{d \in D} \mathcal{Y}_d \times \prod_{c \in C} \mathcal{Y}_c, \bigotimes_{d \in D} \mathcal{B}_{\mathcal{Y}_d} \otimes \bigotimes_{c \in C} \mathcal{B}_{\mathcal{Y}_c})
$$
- $A$ is a measurable cartesian product ([[Cartesian product|link]], [[Measurable set|link]]):
$$
\large
\begin{align}
 & A = \prod_{c \in C} A_c \times \prod_{d \in D} A_d \\
 & A_c = [a_c, b_c] \subseteq \mathbb{R} \\
 & A_d = \{y_{d1}, y_{d2}, \ldots\} \subseteq 2^\mathcal{Y}
\end{align}
$$
- when $i \in D$ :
	- $\large \mathcal{Y}_i = \{y_{i1}, y_{i2}, \ldots \}$ - Countable set of all possible values of $Y$ 
	- $\large \mathcal{B}_{\mathcal{Y}_i} = 2^{\mathcal{Y}} = \{A: A \subseteq \mathcal{Y}\}$ - Collection of all subsets of $\mathcal{Y}_i$ 
- When $i \in C$ :
	- $\mathcal{Y}_i = \mathbb{R}$ 
	- $\large \mathcal{B}_{\mathcal{Y}_i} = \mathcal{B}(\mathbb{R})$ - Borel $\sigma$-algebra ([[Borel sigma algebra|link]])
- $I \subseteq D \cup C$ - Subset of variable indexes with $I^c$ as its complement
- $I_d = I \cap D$ - Subset of indexes for discrete variables
- $I_c = I \cap C$ - Subset of indexes for continuous variables
- $I^c_c, I^c_d$ - Complements of $I_c, I_d$ 
# Equation for the probability of $P(Y_{1:n} \in A \mid x_{1:m})$
Then, for the formal equation for probability, for a multivariate random variable:
$$
\Large
P(\bigwedge_{i=1}^n Y_i \in A_i \mid \bigwedge_{i=1}^m X_i = x_i) = 
\int_{A_{1:n}} p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m}) d\mu_{n:1}(y_{n:1})
$$
we have:
$$
\Large
\int_{A_i} p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m}) d\mu_i(y_i) = 
\begin{cases}
\int_{A_i} p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m}) dy_i, \text{ if } Y_i \text{ - continuous} \\
\sum_{y_i \in A_i} p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m}), \text{ if } Y_i \text{ - discrete}
\end{cases}
$$

So:
$$
\Large
\begin{align}
 & P_{Y_{1:n} \mid X_{1:m}}(\prod_{c \in C} A_c \times \prod_{d \in D} A_d \mid x_{1:m}) = 
 P(Y_C \in \prod_{c \in C} A_c \wedge Y_D \in \prod_{d \in D} A_d \mid \bigwedge_{i=1}^m X_i = x_i) = \\
 & \quad = \sum_{y_D \in \prod_{d \in D} A_d} \int_{\prod_{c \in C} A_c} 
 p_{Y_{1:n} \mid X_{1:m}}(y_C, y_D, \mid x_{1:m}) dy_C
\end{align}
$$
where $\large y_D = (y_d)_{d \in D}$ .
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